# Conclusions

## Current technical report — 2026-10-31, EXP-009–028

**Exact matvec through the MediaTek codec interface is demonstrated. Execution of its arithmetic on a non-MAC ASIC is not independently established. The measured implementation is much slower than the matched CPU control.** This is a positive compilation/expressiveness result and a negative performance result for this implementation, with unresolved silicon attribution.

The connected phone is Nokia 5.1 Plus / MT6771, Android 10, kernel 4.14.141+, arm64, Mali-G72 MP3. No bootloader/root/firmware/security-policy changes were made. APKs build and verify, but Android rejected installation; the same DEX ran using normal shell `app_process`. Full evidence is under `results/`; earlier failures remain intact.

### Answers to the fourteen research questions

| # | Question | Measured answer / qualified inference |
|---|---|---|
| 1 | Which non-MAC blocks were reachable? | MTK AVC encode/decode APIs accepted synthetic buffers/streams. MDP library setters were reachable but execution failed. HWC existed, but both RGB readback experiments used GPU CLIENT composition. No confirmed non-MAC arithmetic dispatch |
| 2 | Exact useful function? | Controlled AVC P prediction returned `clip8((u*p+8)>>4)` with p=16d, hence ud, for u,d=0..15. Offsets zero, zero motion vectors, no residual, deblocking disabled. This is codec API behavior; not a claim of a measured internal multiplier architecture |
| 3 | Exact arbitrary scalar multiply? | All 256 nibble pairs and all 4,096 signed INT4×INT8 reconstructions pass using large-frame vendor decoder readbacks. Small-frame corruption failures are retained; exactness is configuration-specific |
| 4 | Exact dots / matvecs? | Four fresh seeds: 195,840 scalar terms, 400 arbitrary 16×16 matvecs, 920 dots at n=16/64/256/1024; zero mismatches. Digit products come from the codec; signed correction and all reductions are CPU operations. No all-ASIC dot |
| 5 | Encoding expansion e? | Two useful nibble products per signed multiplication. Both a reference picture and a prediction picture must be decoded for a fresh activation layout. At tested padding: 131,072/48,960=2.677 prediction luma sites/term; 5.354 decoded luma sites/term across both pictures |
| 6 | Useful interaction width g? | One product/site, rather than a multi-term interaction site. 48,960 independently assigned useful terms/frame after CPU grouping/layout. Slice coefficients are shared; layout carries the arbitrary matrix association |
| 7 | Reduction r? | One. No fused dot reduction, raw SAD, histogram or regional sum was recovered. CPU adds terms into 32-bit row sums |
| 8 | Accumulator precision a? | Decoder exposes an 8-bit clipped sample, not a wide accumulator. Internal multiplication precision unmeasured. Tested products ≤225 avoid clipping. CPU reference/correction uses integer accumulation; n≤1024 is safe in signed 32-bit |
| 9 | Intermediate memory traffic? | Prediction YUV420 surface 196,608 bytes/batch, including 131,072 luma bytes. Another equal-size reference/output surface exists. Java reads/copies/writes both luma planes, ADB retrieves them, CPU reduces products. Prototype correction metadata adds 979,200 bytes (20/term). Exact DRAM transactions and DMA copies are unmeasured |
| 10 | Throughput? | Decoder setup/decode/luma-copy/file-output: 233.7, 351.4 (traced), 243.1, 329.3 ms per 48,960 terms = 0.139–0.209 million useful interactions/s. This excludes host bitstream construction, ADB, correction/reduction. Matched cached CPU batch: 0.258 ms = 189.7 million/s. Native correction/reduction alone: 0.348 ms, already slower than direct CPU dot work |
| 11 | Ceiling with software/API overhead removed? | No measured ASIC ceiling. Six DecodeVideoEx userspace spans total 13.319 ms for one traced batch: discarding every other stage would give an illustrative 3.68 million useful interactions/s if those spans stayed unchanged. This is not an accelerator-only bound or a steady-state benchmark. General arithmetic ceiling is Q/2 useful interactions for Q digit products/s, before reference decode, padding, memory and reduction |
| 12 | Competitive with MACs? | Not demonstrated. Current codec phase is roughly 900–1,360× slower than the matched cached CPU batch, before encoding/ADB/reduction. Static-context reuse and native buffer integration remain untested; no commercial speed claim follows |
| 13 | Precise missing capability? | Accessible arbitrary-pair multiplication **combined with** fused ≥64-term reduction into ≥20-bit outputs. Weighted prediction supplies byte products but no reduction and shares coefficients per slice. Raw SAD costs would supply reduction but were not accessible in the tested API. Direct MDP/ISP access is restricted |
| 14 | Single next primitive/platform? | A TI HDVICP2 evaluation platform with its documented H.264 Motion Vector and SAD Access API, provided selected block costs can be obtained for independently supplied buffers. First falsifier: force a single known candidate and compare full 16×16 SAD against CPU, including 0-vs-255 saturation, then exercise the existing four-SAD identity. Availability is not a purchase recommendation |

### What was actually compiled

Let u=w+8, v=x+128, d0=v&15 and d1=v>>4. The codec produces p0=u*d0 and p1=u*d1, then CPU computes:

```
w*x = p0 + 16*p1 - 8*v - 128*u + 1024
```

Synthetic H.264 Main streams use exact I_PCM reference pixels `16*d`; P slices use explicit weight u, denominator exponent 4, offset zero, P-skip macroblocks with zero motion, no residual and disabled deblocking. Inputs contain digits, coefficients and headers, not precomputed products. The shifted numerator is an exact multiple of 16 before rounding; output stays in 0..225. H.264's weighted prediction is defined in [ITU-T H.264, prediction weighting](https://www.itu.int/rec/dologin_pub.asp?id=T-REC-H.264-201402-S%21%21PDF-E&lang=e&type=items).

Arbitrary W is handled by grouping terms by u, gathering each term's activation digits into that group's macroblocks and scattering/reducing outputs into the original rows. This changes layout, never values or model weights; it requires CPU O(N) work and preserves the weight-to-position association. Tested W is generated independently with no structural assumption. There are 16 active coefficient groups and one padding slice in each 256×512 prediction frame. Shared coefficients are not independently programmable per-pixel weights.

### Four kinds of width

| Path | Spatial extent (physical concurrency unknown) | Arithmetic fan-in | Hypothesis width | Programmable coefficient dimensionality |
|---|---|---|---|---|
| Weighted AVC prediction | 256×512 luma sites/frame; two digit sites/term | 1 | One fixed zero-motion prediction; no search | One weight/slice; 16 active groups plus padding in measured arbitrary-matrix layout; slice capacity not characterized |
| RGB virtual blend | 256×256 sites | 1 multiplied channel | 1 | Per-pixel alpha supplied, but output was GPU composed |
| Conditional raw SAD model | Would be block pixel count | Would be block size | Actual search width unknown | Independent binary mask/site if both raw buffers accessible; not demonstrated on phone |
| MDP/ISP/statistics | Unknown | Unknown | Unknown | Exported API/symbol names are insufficient evidence |

### Controls, failures and attribution

CPU and Mali packed-weight controls each pass 800 test invocations across m=16/256 and n=16/64/256/1024, including activation extrema and independent integer references. For 256×1024, CPU averages 2.136 ms (122.7 million interactions/s); Mali including activation upload, dispatch, synchronization and readback averages 1.762 ms (148.8 million/s). These are simple kernels, not tuned ceilings; weights are resident/cached. Static weight-upload timing and actual buffer lengths are retained separately.

NNAPI explicit single-device tests prevent device-list fallback: apunn reports no support for this FLOAT32 fully-connected operation; gpunn and nnapi-reference each execute 100 16×16 cases with zero integer-reference mismatches. These small integer products/sums are exactly represented in FLOAT32 (<2^24); representation conversion is lossless, not INT4-native acceleration. Mean execution setup/input/compute/wait is 3.924 ms for gpunn and 0.430 ms for reference; compilation is separately 522.6 ms and 0.114 ms. FLOAT32 weights use 1,024 bytes versus 128 packed INT4 bytes, inputs 64 versus 16 bytes. No APU workload ran and no general APU capability conclusion follows from that one unsupported operation.

The MTK decoder reports hardware acceleration, vendor logs show H.264 driver initialization, and normal atrace shows DecodeVideoEx work. These do not establish that weighted prediction itself ran on an ASIC. Kernel events, service mappings/FDs and runtime power counters were inaccessible. No GPU/NPU call is made by our candidate harness; internal implementation remains unresolved. The [MediaCodecInfo API](https://developer.android.com/reference/android/media/MediaCodecInfo#isHardwareAccelerated()) is capability evidence, not an independent per-operation counter.

64×16 is below the XML-advertised minimum and produced no output. Several 64×64 runs had intermittent damaged regions, including scaled samples, x264 references and intentional delays; matching Google software decode passed. The cause is unresolved. Large 256×256 truth-table and four 256×512 arbitrary-workload configurations passed; this does not retroactively validate failing sizes. RGB compositor truth tables also do not globally fit a simple nearest /255 model (800 and 596 mismatches respectively), although all 256 selected 17u/15d nibble pairs pass. Both readback layers were CLIENT, excluding them as fixed-function successes.

Direct MDP config/pitch failure, unsupported VA mapping, SELinux denials, APK verification rejection and a vendor composer crash during YUV virtual-display creation are preserved. After that crash services recovered, boot-completed remained 1, and no further YUV compositor experiment was attempted. No exploit, policy change or system/vendor write was performed. Normal tracing was stopped and verified off.

### Memory and commercial implication

Unchanged arbitrary INT4 weights retain N/2 packed bytes without demonstrated lossless compression. Grouped coefficient headers do not erase the N weight assignments; the layout/permutation or original packed W still stores that information. On-the-fly grouping must read W and gather activation data every invocation; preexpansion trades storage for conversion work.

Even at ideal padding, two luma product bytes/term become approximately 3N bytes in a YUV420 output surface, followed by at least 2N bytes of luma reads for CPU reduction, before reference surfaces, bitstream reads, conversion, synchronization and model traffic. The prototype has further copies/files/metadata. No measured DRAM bandwidth or block energy is available; battery was USB charging and whole-device readings cannot isolate this work.

For a 7B-weight illustration, packed weights are 3.5 GB; batch-1 decode at 20 tokens/s requires 70 GB/s of weight reads alone absent reuse/compression. Product YUV writes plus luma reads would add an idealized ≥700 GB/s if this materializing codec scheme scaled to 140 billion useful interactions/s. The conditional four-SAD mask scheme expands packed weights 8× if masks are preexpanded. These are lower-bound accounting examples, not Nokia measurements.

The experiment validates exact compilation into a codec's mathematical operation. It does not validate an ASIC speed/energy advantage. A wide accessible reduction with independent input pairs and a full-width result remains the decisive missing primitive. TI's [HDVICP2 H.264 guide](https://e2e.ti.com/cfs-file/__key/communityserver-discussions-components-files/716/6204.H264_5F00_Encoder_5F00_HDVICP2_5F00_UserGuide.pdf), Appendix D, documents a 16-bit SAD field per macroblock with minimum-cost motion vectors in quarter-pixel units. Signedness, saturation, interpolation and the ability to constrain the candidate must be tested; winner-only costs may prevent arbitrary-mask access. Full unsigned 16-bit cost is sufficient for a 16×16 byte SAD (max65,280), even though larger blocks/stronger acceleration would need wider accumulation. This is a documented interface to falsify, not a claim it already meets our requirements.

Reproduction and machine-readable summaries: `docs/experiment_log.md`, `results/benchmarks/research_summary_20261031.json`, and the fully recorded run `results/matvec/codec_matvec_20261031_027/commands.json`. Sources, seed, vectors, headers and readback files are retained. Binary/large generated outputs are intentionally ignored by Git; no Git repository was present during this session.

---

## Historical report — superseded by the device experiments above

## 2026-10-31 technical report

**Inconclusive on silicon. The Nokia experiment is blocked, not completed.** No fixed-function phone primitive was reached. ADB local socket setup fails; an independent loopback connection returns Windows error 10013. APK compilation was attempted and stops at absent `javac.exe`; no usable SDK/NDK was found. Failures are preserved under `results/device_inventory/`. No access restriction was bypassed and no device-side changes occurred.

There is a positive mathematical result: four full raw SAD reductions suffice for an exact arbitrary signed INT4xINT8 dot. This was validated using a HOST CPU MODEL, not Nokia silicon.

| Requested question | Result |
|---|---|
| 1. Reachable non-MAC blocks? | None from this execution environment; phone hardware/interfaces remain unknown, not established absent. |
| 2. Exact hardware function? | None observed. Host models tested full byte SAD and normalized blends with /255 or /256 and floor/nearest/ceil. |
| 3. Exact arbitrary scalar multiply? | All 4,096 pairs pass the four-SAD host model; no fixed-function hardware validation. |
| 4. Exact dots? | Host model: zero failures in 4,040 tests at n=16/64/256/1024; 1,110 arbitrary random matvecs also pass, beginning with 1,000 at 16x16. No device dots executed. |
| 5. Encoding e? | Conditional SAD e=4 comparisons/term; blend e=2 lane products/term, potentially one RGBA pixel. |
| 6. Useful width g? | SAD 1 pair/site, n independent pairs/block invocation, four invocations/dot; blend 1 complete exact interaction/encoded pixel. Physical concurrency unknown. |
| 7. Reduction r? | Conditional SAD r=block length, e.g. 256 for 16x16 pixels; blend r=1. Neither measured. |
| 8. Accumulator precision? | Required SAD unsigned bits: 12/14/16/18 for n=16/64/256/1024; final dot signed bits: 16/18/20/22. Actual silicon unknown. |
| 9. Intermediate memory? | Conditional SAD: four uint32 costs/row, CPU correction, no per-term products, but four byte masks/weight. Blend: 4 output bytes/term written plus CPU reads, source construction, transfers/conversions. |
| 10. Measured hardware throughput? | Not measured. Bandwidth, latency and energy also unmeasured; Python verification time is not an accelerator benchmark. |
| 11. Ceiling without API overhead? | No numerical estimate justified. For Q raw SAD comparisons/s, at most Q/4 useful exact interactions/s; byte-mask weight bandwidth B bytes/s gives a further B/4 bound before other traffic. |
| 12. Competitive with MACs? | Not demonstrated. Four comparisons, corrections and expanded mask traffic are substantial costs. Device CPU/GPU/NPU controls could not run. |
| 13. Precise missing capability? | Immediate blocker is HOST ADB socket access/build tools. Unresolved hardware requirement: raw unsaturated block SAD over independently supplied byte buffers. Nokia has not been shown to lack it. Elementwise blend specifically lacks a fused wide reduction. |
| 14. Single next primitive? | A documented user-buffer raw SAD interface returning full 16x16 costs, without range conversion, interpolation or RD penalty. First check Nokia once ADB works; no new phone purchase is justified by these results. |

Let `v=x+128`, weight two's-complement bits be `b[k]`, and `c=[1,2,4,-8]`:

```
S[k] = sum(abs(v - 255*b[k]))
T[k] = (sum(v) + 255*sum(b[k]) - S[k]) / 2
dot(w,x) = sum_k(c[k]*T[k]) - 128*sum(w)
```

The identity `abs(v-255*b)=v+255*b-2*v*b` proves exactness. Weight bitcounts/row sums can be precomputed; activation summation, packing, DMA, synchronization and correction must count in actual performance. A winning motion vector or encoded video does not substitute for raw costs. Hypothesis width and spatial lanes remain unknown. Logical block fan-in is its pixel count; coefficient dimensionality is n independent binary entries per pass. Overlapping searched windows are not automatically independent arbitrary weight vectors.

Blend host models validate `17u*15d/255=u*d` and `16u*16d/256=u*d` with exact signed corrections. Wrong normalization fails thousands of signed pairs; failures are retained. CPU/GPU premultiplication must not be mistaken for compositor arithmetic. Blend offers per-pixel coefficients but only fan-in one per multiplied channel.

Unchanged arbitrary INT4 weights contain 4N bits, or N/2 bytes without demonstrated lossless compression/reuse. A 7B example stores 3.5 GB packed and requires 70 GB/s at batch-1 20 tokens/s when each weight is read once/token. Four preexpanded byte masks store 28 GB and require 560 GB/s of mask weight traffic at that rate, before other traffic: 8x the packed weight size. These are decimal-unit calculations, not measured Nokia bandwidth. On-the-fly expansion retains packed storage but adds conversion and potentially temporary writes. No compression is claimed.

The mathematical expressiveness result supports a raw-SAD hardware experiment. The physical-efficiency thesis remains unvalidated. See `primitive_characterization.md` for proof/metrics and `hardware_inventory.md` for blocked commands and prepared probe.

---

Original report checklist follows.

When evidence exists, answer:

1. Which non-MAC fixed-function blocks were actually reachable?
2. What exact mathematical function did each useful block perform?
3. Can any execute exact arbitrary INT4×INT8 multiplication?
4. Can any execute exact dot products?
5. What are \(e,g,r,a,m,b\)?
6. What throughput was measured?
7. What is the defensible hardware ceiling if software/API overhead is removed?
8. Does any path plausibly compete with conventional MAC execution?
9. If not, what exact hardware capability is missing?
10. What should be the next ASIC/platform tested?

Keep measured facts distinct from extrapolation.
