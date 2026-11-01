# Non-MAC Matmul Lab

Experimental project for testing whether **exact arbitrary neural-network matrix multiplication** can be recast onto **commodity non-MAC fixed-function ASICs** such as ISP, video codec, motion-estimation, image-statistics, compositor, depth/stereo, scaler, DSP, or similar blocks.

Initial device: **Nokia 5.1 Plus**, expected MediaTek Helio P60 / MT6771.

## Core thesis

Given unchanged quantized model weights, can we compile

\[
y = Wx
\]

into the native arithmetic of a fixed-function ASIC so that it remains **bit-exact** while materially improving physical efficiency versus conventional MAC-centric execution?

This project is **not** primarily about running an LLM on an old phone. The phone is a cheap experimental platform for discovering useful hardware algebra.

## Hard constraints

- No retraining or model approximation for the primary thesis.
- Arbitrary signed INT4 weights and signed INT8 activations are the first target.
- Exactness is always checked against a CPU integer reference.
- Weight information is not assumed compressible.
- All transfer, conversion, synchronization, and reduction overhead counts.
- No root, bootloader unlock, flashing, exploits, or persistent system modification unless the project owner explicitly changes this rule.

## Start here

Agents should read, in order:

1. `AGENTS.md`
2. `PROJECT.md`
3. `EXPERIMENT_PROTOCOL.md`
4. `TASK.md`
5. `STATUS.md`

Experimental evidence belongs under `results/`; durable conclusions belong under `docs/`.
