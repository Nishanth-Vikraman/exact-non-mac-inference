# Exact INT4 x INT8 RTL comparison: provisional results

As of 2026-10-31 22:55 IST, 147 of 150 mapped synthesis points are available.
The independent Windows scheduled task completed serial bitplanes at LANES=256,
then full-LUT LANES=256 synthesis preparation timed out after 1,800 seconds.
All three timing targets for that geometry are missing. The worker stopped with
a recorded failure at 22:29 IST. No failed run was restarted for this summary.

The implemented SAD, bitplane and LUT designs all lose to conventional MACs on
mapped cell area per matched useful throughput. The best measured engine is
Booth recoding: 0.9284x the best MAC tile's area/throughput, a 7.2% improvement.
Booth is conventional multiplier arithmetic; this is not a non-MAC breakthrough.
No measured candidate reaches the mission's interesting threshold below 0.8x.

Each architecture selects its best available tile across the same five lane
counts and three optimization targets. The MAC reference can also select and
replicate its best tile. Ratios use ideal many-tile throughput matching, rather
than comparing raw areas. The incomplete full-LUT row uses only LANES<=128.

| Architecture | Selected LANES | Area / useful throughput vs best MAC |
|---|---:|---:|
| A1 multiplier + tree | 16 | 1.0000x |
| A2 partial accumulation | 128 | 1.1854x |
| B1 four-SAD, derived constants | 128 | 1.7701x |
| B2 four-SAD, precomputed row constant | 32 | 1.4025x |
| C1 parallel AND/popcounts | 32 | 2.1540x |
| C2 serial bitplanes | 32 | 3.3073x |
| D1 full LUT, incomplete sweep | 16 | 1.2827x |
| D2 segmented LUT | 128 | 1.4006x |
| E1 Booth recoding | 32 | 0.9284x |
| E2 explicit carry-save partial products | 32 | 0.9914x |

## Exactness and limits

All 90 primary RTL configurations pass 1,000 randomized vectors plus six directed
vectors each: 90,540 dot outputs and 219,710,400 original INT4 x INT8 interactions,
with zero mismatches. N=16/64/256/1024/4096 are covered at LANES=16; N=4096 also
covers LANES=32/64/128/256. This is not the full Cartesian product of N and LANES.
All 4,096 scalar combinations pass the five product implementations; four
alternative product forms pass scalar SAT equivalence against multiplication.
Fifty continuous-input configurations verify cadence. All ten streaming engines
also pass embedded scalar tests, and all ten pass Verilator lint at LANES=256.

Mapped simulation at LANES=16 passes nine engines with ordinary four-state
initialization. The serial bitplane mapped replay fails to emit outputs under
X initialization. Replays initialized to zero and one pass; SAT proves control
reset for every binary initial state. The X-initialized failure remains preserved
and qualifies the serial engine's mapped verification. No completed full-matrix
final validation or final experiment commit is claimed.

All area is a SKY130 HD TT/25C/1.8V standard-cell sum. Frequency and throughput
use ABC combinational delay with common buf_2 drivers and 3 fF loads, capped by
the requested clock. Actual flip-flop clock-Q/setup, placement, routing and clock
distribution are excluded. These are optimistic pre-layout proxies, not signoff
clocks or measured silicon throughput. No power or manufacturing-cost estimate
is available, and absolute SKY130 performance is not a modern-node prediction.

## What the measurements imply

Four-SAD's inexpensive endpoint distances do not compensate for four distance
reductions, the activation reduction, correction arithmetic and pipeline state.
Parallel bitplanes spend more area in reductions, registers and reconstruction;
serial bitplanes save raw area but accept a packed beat only once every four
cycles and have a slow combinational path. Throughput normalization removes the
apparent serial-area advantage. These are measured architecture-level outcomes,
not formal lower bounds on every possible implementation.

LUT descriptions map differently and more expensively than inferred multipliers
at completed points. Synthesis does not recover an equally efficient multiplier
from these descriptions. The missing largest full-LUT geometry prevents a final
claim about its complete sweep; its timeout is a tool-flow limitation, not an
arithmetic exactness failure.

The same engine minimizes area per useful interaction/s and per 4096-wide dot/s:
one exact dot is always 4096 useful interactions. In the selected Booth L32 tile,
flip-flops contribute 42.9% of cell area and XOR/XNOR cells 19.9%. Its reported
critical path runs from a registered reduction-tree output to dot-accumulator
bit 23. Carry propagation in accumulation is a promising next target. A fused
signed partial-product bit heap with carry-save accumulation should be compared
against a MAC baseline receiving the same reduction/accumulation improvements.

All cores accept original packed 4-bit weights and 8-bit activations, with
conversion logic included. Only B2 adds persistent metadata: 16 bits per 4096
weights, a 1.0009765625x total weight-storage ratio. No system-memory advantage
is demonstrated; weight reuse is also available to MACs.

These results weaken the tested SAD/popcount/LUT routes to fundamentally cheaper
exact inference arithmetic. They do not justify an ASIC on demonstrated arithmetic
cost advantage alone, and do not falsify every future exact architecture or the
separate idea of repurposing an existing commodity ASIC. Routed PPA and power
remain unmeasured. The current evidence is a bounded negative result.

Complete available lane/target tables: [rtl_results.md](rtl_results.md).
Machine-readable results: results/rtl/sweeps/summary.json and summary.csv.
Cell families and paths: results/rtl/sweeps/structure.json. Raw failures and all
prior Nokia evidence are preserved.
