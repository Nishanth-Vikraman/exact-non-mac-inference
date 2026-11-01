# Exact INT4 x INT8 RTL comparison

The comparison concerns arithmetic cores built from the same SKY130 HD cells,
TT / 25 C / 1.8 V. It does not estimate modern-node die cost or reproduce a GPU.

## Contract and interface

`dot_top` takes signed two's-complement packed 4-bit weights and 8-bit activations,
lane 0 in the least-significant bits. Parameters are DOT_N (default 4096),
LANES (16/32/64/128/256), and ARCH. Current supported configurations require
DOT_N divisible by LANES and power-of-two LANES; A2 requires LANES >= 4.
Only `in_valid && in_ready` advances the dot counter. Reset discards an incomplete
dot. Output is an exact sign-extended INT32 with `out_valid`; the consumer accepts
all output beats (there is no output backpressure). Inputs may contain bubbles.
`row_sumw` is used only by B2 and is valid on the first accepted beat of each row.

The product fits 12 signed bits. Tested dot extrema for N=4096 fit 24 signed bits
(maximum +4,194,304). Accumulators are 12+ceil(log2(DOT_N)) bits; B2 has one
additional numerator bit. A2 partial accumulators use their actual term-count bound.
The same arithmetic contract applies to every engine.

## Implementations

| ID | Architecture | Initiation interval per original input beat | Structure |
|---|---|---:|---|
| 0 A1 | MAC tree | 1 | Input registers, signed inferred multipliers, product registers, pipelined balanced sum tree, dot accumulator |
| 1 A2 | MAC partial | 1 | Same multipliers, groups of four reduce, registered per-group dot accumulation, final pipelined group reduction |
| 2 B1 | SAD derived | 1 | Four endpoint-distance reductions, unsigned activation sum and signed weight sum from packed inputs, exact reconstruction, accumulation |
| 3 B2 | SAD precomputed | 1 | Four distance reductions and activation sum, numerator accumulation; signed row-weight-sum correction once per dot |
| 4 C1 | Parallel bitplanes | 1 | 32 AND/popcount trees, fixed signed shifts and pipelined balanced reconstruction |
| 5 C2 | Serial bitplanes | 4 | Holds the original packed beat, processes one weight bit with eight activation planes/cycle, reconstructs four phases |
| 6 D1 | Full LUT | 1 | Exhaustive 16 x 256 combinational case table per lane, then same product registers/reduction as A1 |
| 7 D2 | Segmented LUT | 1 | Two 16 x 16 tables: signed weight times unsigned low nibble and signed high nibble; exact shift/add, same reduction as A1 |
| 8 E1 | Booth | 1 | Two radix-four signed digits selecting 0, +/-x, +/-2x; exact reconstruction, A1 reduction |
| 9 E2 | CSA product | 1 | Four signed partial products, explicit two carry-save stages and final carry-propagate addition, A1 reduction |

C2 accepts LANES original terms every four cycles, not LANES useful interactions
every cycle. Throughput normalization must include that factor. No bitplanes or
SAD masks enter through memory. Fully parallel engines accept a new original beat
each cycle and a new dot immediately after the preceding dot's last beat.

## Four-SAD algebra and metadata

For u=x+128, endpoint distance |u-255*b| is `u XOR {8{b}}`; x+128 is a sign-bit
flip. With c=[1,2,4,-8], sum(c)=-1. Substituting the specified T identity gives

    2*dot = -sum(u) - (S0 + 2*S1 + 4*S2 - 8*S3) - sum(w).

This removes redundant plane-count arithmetic without changing the four SAD paths.
B1 computes sum(w) per beat internally and shifts its always-even numerator.
B2 accumulates the numerator and subtracts the row constant before the exact shift.
Only sum(w), a signed 16-bit value for N=4096, must be stored: 16 bits/row,
0.00390625 bits/weight. If all four bit counts were stored independently they
would need 4*13=52 bits/row; independently storing sum(w) too would total 68.
Those redundant forms are not charged to the optimized implementation.

## Representation accounting

Every model row remains 16,384 original weight bits. Engines other than B2 have
zero persistent metadata; B2's storage ratio is 16,400/16,384=1.0009765625.
Nonstationary weight bandwidth is 4 bits per useful interaction, plus 16/4096
bits for B2. Activation bandwidth is 8 bits/interaction. C1 constructs 32*LANES
one-bit correlations; C2 constructs 8*LANES per phase. SAD constructs 4*8*LANES
endpoint-distance bits plus 8*LANES unsigned activations. These are internal wires
and registers included in the synthesized core, not free memory representations.
LUT tables are combinational logic included in cell area, not model-specific ROMs.
The source's nominal D1 truth table is 49,152 bits per lane; D2 is 4,096 bits/lane,
but mapped logic area, rather than that source representation, is measured.

In weight-stationary high-batch use, packed weights can be held and reused. This
reduces external weight traffic for every architecture; reuse does not establish
a memory advantage for a particular arithmetic identity. This initial core sweep
includes input registers but excludes SRAM macros, DRAM controllers, chip I/O,
clock tree, DMA and host/runtime. System traffic and manufacturing cost remain
separate from arithmetic-core area/throughput.

## Tool and measurement policy

The official Windows OSS CAD Suite release is pinned by tools/toolchain.lock.json.
The downloaded archive hash and Liberty Git-blob hash were checked. Driver crashes
are retained under results/rtl/bootstrap and early functional runs. Icarus's same
packaged ivlpp/ivl binaries are invoked sequentially instead of its failing driver
pipeline. No Linux/WSL or global installation is used.

All designs use the same flat Yosys synthesis and ABC Liberty mapping, constraints,
and 10,000/4,000/2,000 ps delay targets. Datapath registers are not reset; valid and
state control are. No retiming of sequential state is requested. ABC sees register
boundaries as combinational inputs/outputs. Its delay is a mapped combinational
proxy with identical buf_2 drivers and 3 fF loads, not signoff Fmax: it excludes
actual launching FF clock-Q, receiving FF setup, extracted routing and clock skew.
Results must state this limitation and unmet targets, not equate target clocks
with achieved clocks. Power and routed physical results are pending.
