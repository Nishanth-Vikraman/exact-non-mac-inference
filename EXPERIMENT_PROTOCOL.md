# Experiment Protocol

## Reference semantics

The baseline arithmetic is exact signed integer math.

Start with:

- weight: signed INT4, values `[-8, 7]`;
- activation: signed INT8, values `[-128, 127]`;
- accumulation: wide enough to prevent overflow for the tested vector length.

Every candidate hardware result must be compared with a CPU reference using the same defined arithmetic.

## Progression

### A. Primitive characterization

For the candidate block:

- determine exact input/output formats;
- enumerate small-domain behavior when feasible;
- characterize rounding, saturation, clipping, signedness, normalization, boundary behavior, coefficient precision, and hidden state;
- prove that the intended hardware block executed.

### B. Exact scalar multiply

Implement:

\[
w\cdot x
\]

for signed INT4 × signed INT8.

Prefer exhaustive validation over all \(16\times256=4096\) scalar input pairs.

### C. Exact dot product

Test lengths:

- 16
- 64
- 256
- 1024
- larger only if useful

Include random vectors and adversarial extrema.

### D. Exact arbitrary matvec

Start with arbitrary random \(16\times16\) INT4 matrices and scale only after exactness is established.

No structural assumptions about \(W\).

### E. Controls

Benchmark equivalent work on:

- CPU;
- GPU if accessible;
- NNAPI/APU if accessible.

Controls must not be confused with the candidate non-MAC execution path.

## Candidate exact encodings

These are hypotheses, not assumptions.

### Normalized blend

If hardware implements a known fixed-point blend such as

\[
B(a,s)=\operatorname{round}(as/255),
\]

test mappings that make small integer multiplication exact. Exhaustively determine real hardware rounding/normalization first.

### Bit planes

Explore exact multiplication through Boolean/mask/LUT/compare/reduce primitives when unusually wide.

### Convolution/filter embedding

Measure true coefficient independence. Globally shared kernels do not provide arbitrary dense-matrix programmability.

### Motion/block matching

Look for many pairwise operations plus fused reductions, and whether raw candidate costs can be recovered.

### Statistics/reduction

Regional sums, histograms, moments, correlations, and block accumulators may be more valuable than raw elementwise arithmetic.

## Benchmark accounting

Record:

- dimensions;
- datatype;
- number of candidate-hardware invocations;
- encoding/decoding work;
- host↔device transfers;
- internal/external buffer copies when known;
- synchronization;
- intermediate bytes;
- latency distribution;
- throughput;
- accumulator width;
- exactness failures;
- energy if measurable.

Never report only the inner primitive time if end-to-end execution requires substantial additional work.

## Evidence standard

A result is **confirmed** only when reproducible raw evidence exists under `results/`.

A negative result is valuable when it identifies the exact limiting hardware property.
