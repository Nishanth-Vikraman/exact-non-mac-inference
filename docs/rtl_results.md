# Mapped RTL results

All area is standard-cell area in um^2. Fmax* and throughput* are ABC combinational timing proxies, not signoff achievable clocks. They exclude actual FF clock-Q/setup and extracted physical timing. Throughput uses min(target clock, Fmax*); no power estimate is made. All listed rows passed 1,000 randomized exact vectors plus directed cases before synthesis.

Matched area uses ideal replication in the many-tile limit. CSV also gives integer replicas and overprovisioned area for matching one baseline core. Pipeline latency/cadence are measured separately with continuous inputs.

## Target 100 MHz (10000 ps)

### LANES = 16

| Architecture | LANES | Area um2 | Fmax* MHz | Cycles/dot | Dots/s* | Interactions/s* | Area @ matched throughput* | Metadata bits/row | Exact? |
|---|---:|---:|---:|---:|---:|---:|---:|---:|---|
| A1_mac_tree | 16 | 33661.0 | 175.73 | 256 | 390625 | 1.6e+09 | 33661.0 | 0 | Yes, tested |
| A2_mac_partial | 16 | 39102.5 | 158.40 | 256 | 390625 | 1.6e+09 | 39102.5 | 0 | Yes, tested |
| B1_sad_derived | 16 | 49711.4 | 138.81 | 256 | 390625 | 1.6e+09 | 49711.4 | 0 | Yes, tested |
| B2_sad_precomputed | 16 | 49846.6 | 177.13 | 256 | 390625 | 1.6e+09 | 49846.6 | 16 | Yes, tested |
| C1_bitplane_parallel | 16 | 65741.8 | 150.12 | 256 | 390625 | 1.6e+09 | 65741.8 | 0 | Yes, tested |
| C2_bitplane_serial | 16 | 16345.7 | 104.40 | 1024 | 97656 | 4e+08 | 65382.7 | 0 | Yes, tested |
| D1_lut_full | 16 | 48103.6 | 197.10 | 256 | 390625 | 1.6e+09 | 48103.6 | 0 | Yes, tested |
| D2_lut_segmented | 16 | 45967.8 | 166.02 | 256 | 390625 | 1.6e+09 | 45967.8 | 0 | Yes, tested |
| E1_booth | 16 | 31301.3 | 172.48 | 256 | 390625 | 1.6e+09 | 31301.3 | 0 | Yes, tested |
| E2_csa | 16 | 34508.1 | 175.67 | 256 | 390625 | 1.6e+09 | 34508.1 | 0 | Yes, tested |

| Architecture | Area ratio | Throughput ratio* | Area/throughput ratio* | Delay ratio | Storage ratio |
|---|---:|---:|---:|---:|---:|
| A1_mac_tree | 1.000 | 1.000 | 1.000 | 1.000 | 1.000000 |
| A2_mac_partial | 1.162 | 1.000 | 1.162 | 1.109 | 1.000000 |
| B1_sad_derived | 1.477 | 1.000 | 1.477 | 1.266 | 1.000000 |
| B2_sad_precomputed | 1.481 | 1.000 | 1.481 | 0.992 | 1.000977 |
| C1_bitplane_parallel | 1.953 | 1.000 | 1.953 | 1.171 | 1.000000 |
| C2_bitplane_serial | 0.486 | 0.250 | 1.942 | 1.683 | 1.000000 |
| D1_lut_full | 1.429 | 1.000 | 1.429 | 0.892 | 1.000000 |
| D2_lut_segmented | 1.366 | 1.000 | 1.366 | 1.058 | 1.000000 |
| E1_booth | 0.930 | 1.000 | 0.930 | 1.019 | 1.000000 |
| E2_csa | 1.025 | 1.000 | 1.025 | 1.000 | 1.000000 |

### LANES = 32

| Architecture | LANES | Area um2 | Fmax* MHz | Cycles/dot | Dots/s* | Interactions/s* | Area @ matched throughput* | Metadata bits/row | Exact? |
|---|---:|---:|---:|---:|---:|---:|---:|---:|---|
| A1_mac_tree | 32 | 65097.4 | 169.16 | 128 | 781250 | 3.2e+09 | 65097.4 | 0 | Yes, tested |
| A2_mac_partial | 32 | 77184.0 | 161.76 | 128 | 781250 | 3.2e+09 | 77184.0 | 0 | Yes, tested |
| B1_sad_derived | 32 | 97224.5 | 128.27 | 128 | 781250 | 3.2e+09 | 97224.5 | 0 | Yes, tested |
| B2_sad_precomputed | 32 | 93776.2 | 175.11 | 128 | 781250 | 3.2e+09 | 93776.2 | 16 | Yes, tested |
| C1_bitplane_parallel | 32 | 122682.7 | 148.63 | 128 | 781250 | 3.2e+09 | 122682.7 | 0 | Yes, tested |
| C2_bitplane_serial | 32 | 27964.3 | 100.48 | 512 | 195312 | 8e+08 | 111857.3 | 0 | Yes, tested |
| D1_lut_full | 32 | 93711.1 | 150.57 | 128 | 781250 | 3.2e+09 | 93711.1 | 0 | Yes, tested |
| D2_lut_segmented | 32 | 90232.8 | 158.56 | 128 | 781250 | 3.2e+09 | 90232.8 | 0 | Yes, tested |
| E1_booth | 32 | 60546.8 | 170.21 | 128 | 781250 | 3.2e+09 | 60546.8 | 0 | Yes, tested |
| E2_csa | 32 | 66819.1 | 175.68 | 128 | 781250 | 3.2e+09 | 66819.1 | 0 | Yes, tested |

| Architecture | Area ratio | Throughput ratio* | Area/throughput ratio* | Delay ratio | Storage ratio |
|---|---:|---:|---:|---:|---:|
| A1_mac_tree | 1.000 | 1.000 | 1.000 | 1.000 | 1.000000 |
| A2_mac_partial | 1.186 | 1.000 | 1.186 | 1.046 | 1.000000 |
| B1_sad_derived | 1.494 | 1.000 | 1.494 | 1.319 | 1.000000 |
| B2_sad_precomputed | 1.441 | 1.000 | 1.441 | 0.966 | 1.000977 |
| C1_bitplane_parallel | 1.885 | 1.000 | 1.885 | 1.138 | 1.000000 |
| C2_bitplane_serial | 0.430 | 0.250 | 1.718 | 1.684 | 1.000000 |
| D1_lut_full | 1.440 | 1.000 | 1.440 | 1.123 | 1.000000 |
| D2_lut_segmented | 1.386 | 1.000 | 1.386 | 1.067 | 1.000000 |
| E1_booth | 0.930 | 1.000 | 0.930 | 0.994 | 1.000000 |
| E2_csa | 1.026 | 1.000 | 1.026 | 0.963 | 1.000000 |

### LANES = 64

| Architecture | LANES | Area um2 | Fmax* MHz | Cycles/dot | Dots/s* | Interactions/s* | Area @ matched throughput* | Metadata bits/row | Exact? |
|---|---:|---:|---:|---:|---:|---:|---:|---:|---|
| A1_mac_tree | 64 | 128105.4 | 153.13 | 64 | 1562500 | 6.4e+09 | 128105.4 | 0 | Yes, tested |
| A2_mac_partial | 64 | 151708.0 | 158.28 | 64 | 1562500 | 6.4e+09 | 151708.0 | 0 | Yes, tested |
| B1_sad_derived | 64 | 192437.1 | 138.15 | 64 | 1562500 | 6.4e+09 | 192437.1 | 0 | Yes, tested |
| B2_sad_precomputed | 64 | 181394.0 | 145.60 | 64 | 1562500 | 6.4e+09 | 181394.0 | 16 | Yes, tested |
| C1_bitplane_parallel | 64 | 237162.5 | 137.77 | 64 | 1562500 | 6.4e+09 | 237162.5 | 0 | Yes, tested |
| C2_bitplane_serial | 64 | 51424.3 | 94.30 | 256 | 368360 | 1.509e+09 | 218130.2 | 0 | Yes, tested |
| D1_lut_full | 64 | 185392.8 | 153.98 | 64 | 1562500 | 6.4e+09 | 185392.8 | 0 | Yes, tested |
| D2_lut_segmented | 64 | 177879.4 | 154.08 | 64 | 1562500 | 6.4e+09 | 177879.4 | 0 | Yes, tested |
| E1_booth | 64 | 118841.5 | 158.24 | 64 | 1562500 | 6.4e+09 | 118841.5 | 0 | Yes, tested |
| E2_csa | 64 | 131219.6 | 168.69 | 64 | 1562500 | 6.4e+09 | 131219.6 | 0 | Yes, tested |

| Architecture | Area ratio | Throughput ratio* | Area/throughput ratio* | Delay ratio | Storage ratio |
|---|---:|---:|---:|---:|---:|
| A1_mac_tree | 1.000 | 1.000 | 1.000 | 1.000 | 1.000000 |
| A2_mac_partial | 1.184 | 1.000 | 1.184 | 0.967 | 1.000000 |
| B1_sad_derived | 1.502 | 1.000 | 1.502 | 1.108 | 1.000000 |
| B2_sad_precomputed | 1.416 | 1.000 | 1.416 | 1.052 | 1.000977 |
| C1_bitplane_parallel | 1.851 | 1.000 | 1.851 | 1.111 | 1.000000 |
| C2_bitplane_serial | 0.401 | 0.236 | 1.703 | 1.624 | 1.000000 |
| D1_lut_full | 1.447 | 1.000 | 1.447 | 0.994 | 1.000000 |
| D2_lut_segmented | 1.389 | 1.000 | 1.389 | 0.994 | 1.000000 |
| E1_booth | 0.928 | 1.000 | 0.928 | 0.968 | 1.000000 |
| E2_csa | 1.024 | 1.000 | 1.024 | 0.908 | 1.000000 |

### LANES = 128

| Architecture | LANES | Area um2 | Fmax* MHz | Cycles/dot | Dots/s* | Interactions/s* | Area @ matched throughput* | Metadata bits/row | Exact? |
|---|---:|---:|---:|---:|---:|---:|---:|---:|---|
| A1_mac_tree | 128 | 253768.4 | 148.71 | 32 | 3125000 | 1.28e+10 | 253768.4 | 0 | Yes, tested |
| A2_mac_partial | 128 | 299205.7 | 166.82 | 32 | 3125000 | 1.28e+10 | 299205.7 | 0 | Yes, tested |
| B1_sad_derived | 128 | 382657.0 | 141.40 | 32 | 3125000 | 1.28e+10 | 382657.0 | 0 | Yes, tested |
| B2_sad_precomputed | 128 | 356552.0 | 142.73 | 32 | 3125000 | 1.28e+10 | 356552.0 | 16 | Yes, tested |
| C1_bitplane_parallel | 128 | 465730.4 | 138.70 | 32 | 3125000 | 1.28e+10 | 465730.4 | 0 | Yes, tested |
| C2_bitplane_serial | 128 | 96533.8 | 82.72 | 128 | 646255 | 2.647e+09 | 466794.4 | 0 | Yes, tested |
| D1_lut_full | 128 | 369120.3 | 139.81 | 32 | 3125000 | 1.28e+10 | 369120.3 | 0 | Yes, tested |
| D2_lut_segmented | 128 | 353952.0 | 163.67 | 32 | 3125000 | 1.28e+10 | 353952.0 | 0 | Yes, tested |
| E1_booth | 128 | 235173.0 | 153.00 | 32 | 3125000 | 1.28e+10 | 235173.0 | 0 | Yes, tested |
| E2_csa | 128 | 260325.9 | 170.39 | 32 | 3125000 | 1.28e+10 | 260325.9 | 0 | Yes, tested |

| Architecture | Area ratio | Throughput ratio* | Area/throughput ratio* | Delay ratio | Storage ratio |
|---|---:|---:|---:|---:|---:|
| A1_mac_tree | 1.000 | 1.000 | 1.000 | 1.000 | 1.000000 |
| A2_mac_partial | 1.179 | 1.000 | 1.179 | 0.891 | 1.000000 |
| B1_sad_derived | 1.508 | 1.000 | 1.508 | 1.052 | 1.000000 |
| B2_sad_precomputed | 1.405 | 1.000 | 1.405 | 1.042 | 1.000977 |
| C1_bitplane_parallel | 1.835 | 1.000 | 1.835 | 1.072 | 1.000000 |
| C2_bitplane_serial | 0.380 | 0.207 | 1.839 | 1.798 | 1.000000 |
| D1_lut_full | 1.455 | 1.000 | 1.455 | 1.064 | 1.000000 |
| D2_lut_segmented | 1.395 | 1.000 | 1.395 | 0.909 | 1.000000 |
| E1_booth | 0.927 | 1.000 | 0.927 | 0.972 | 1.000000 |
| E2_csa | 1.026 | 1.000 | 1.026 | 0.873 | 1.000000 |

### LANES = 256

| Architecture | LANES | Area um2 | Fmax* MHz | Cycles/dot | Dots/s* | Interactions/s* | Area @ matched throughput* | Metadata bits/row | Exact? |
|---|---:|---:|---:|---:|---:|---:|---:|---:|---|
| A1_mac_tree | 256 | 504094.7 | 151.70 | 16 | 6250000 | 2.56e+10 | 504094.7 | 0 | Yes, tested |
| A2_mac_partial | 256 | 589515.4 | 157.16 | 16 | 6250000 | 2.56e+10 | 589515.4 | 0 | Yes, tested |
| B1_sad_derived | 256 | 763438.4 | 139.46 | 16 | 6250000 | 2.56e+10 | 763438.4 | 0 | Yes, tested |
| B2_sad_precomputed | 256 | 706513.9 | 133.29 | 16 | 6250000 | 2.56e+10 | 706513.9 | 16 | Yes, tested |
| C1_bitplane_parallel | 256 | 923366.8 | 127.76 | 16 | 6250000 | 2.56e+10 | 923366.8 | 0 | Yes, tested |
| C2_bitplane_serial | 256 | 186049.7 | 74.79 | 64 | 1168556 | 4.786e+09 | 995083.0 | 0 | Yes, tested |
| D2_lut_segmented | 256 | 705726.8 | 146.54 | 16 | 6250000 | 2.56e+10 | 705726.8 | 0 | Yes, tested |
| E1_booth | 256 | 468052.6 | 147.14 | 16 | 6250000 | 2.56e+10 | 468052.6 | 0 | Yes, tested |
| E2_csa | 256 | 518690.0 | 146.83 | 16 | 6250000 | 2.56e+10 | 518690.0 | 0 | Yes, tested |

| Architecture | Area ratio | Throughput ratio* | Area/throughput ratio* | Delay ratio | Storage ratio |
|---|---:|---:|---:|---:|---:|
| A1_mac_tree | 1.000 | 1.000 | 1.000 | 1.000 | 1.000000 |
| A2_mac_partial | 1.169 | 1.000 | 1.169 | 0.965 | 1.000000 |
| B1_sad_derived | 1.514 | 1.000 | 1.514 | 1.088 | 1.000000 |
| B2_sad_precomputed | 1.402 | 1.000 | 1.402 | 1.138 | 1.000977 |
| C1_bitplane_parallel | 1.832 | 1.000 | 1.832 | 1.187 | 1.000000 |
| C2_bitplane_serial | 0.369 | 0.187 | 1.974 | 2.028 | 1.000000 |
| D2_lut_segmented | 1.400 | 1.000 | 1.400 | 1.035 | 1.000000 |
| E1_booth | 0.929 | 1.000 | 0.929 | 1.031 | 1.000000 |
| E2_csa | 1.029 | 1.000 | 1.029 | 1.033 | 1.000000 |

## Target 250 MHz (4000 ps)

### LANES = 16

| Architecture | LANES | Area um2 | Fmax* MHz | Cycles/dot | Dots/s* | Interactions/s* | Area @ matched throughput* | Metadata bits/row | Exact? |
|---|---:|---:|---:|---:|---:|---:|---:|---:|---|
| A1_mac_tree | 16 | 33747.4 | 209.64 | 256 | 818910 | 3.354e+09 | 33747.4 | 0 | Yes, tested |
| A2_mac_partial | 16 | 39230.1 | 193.43 | 256 | 755567 | 3.095e+09 | 42519.0 | 0 | Yes, tested |
| B1_sad_derived | 16 | 49791.5 | 166.12 | 256 | 648895 | 2.658e+09 | 62837.2 | 0 | Yes, tested |
| B2_sad_precomputed | 16 | 49969.2 | 213.50 | 256 | 833970 | 3.416e+09 | 49066.8 | 16 | Yes, tested |
| C1_bitplane_parallel | 16 | 65828.1 | 178.79 | 256 | 698406 | 2.861e+09 | 77186.2 | 0 | Yes, tested |
| C2_bitplane_serial | 16 | 16592.2 | 117.50 | 1024 | 114745 | 4.7e+08 | 118415.1 | 0 | Yes, tested |
| D1_lut_full | 16 | 48255.0 | 233.70 | 256 | 912882 | 3.739e+09 | 43287.7 | 0 | Yes, tested |
| D2_lut_segmented | 16 | 46093.0 | 197.97 | 256 | 773320 | 3.168e+09 | 48810.3 | 0 | Yes, tested |
| E1_booth | 16 | 31382.6 | 204.94 | 256 | 800546 | 3.279e+09 | 32102.5 | 0 | Yes, tested |
| E2_csa | 16 | 34594.4 | 209.60 | 256 | 818733 | 3.354e+09 | 34601.9 | 0 | Yes, tested |

| Architecture | Area ratio | Throughput ratio* | Area/throughput ratio* | Delay ratio | Storage ratio |
|---|---:|---:|---:|---:|---:|
| A1_mac_tree | 1.000 | 1.000 | 1.000 | 1.000 | 1.000000 |
| A2_mac_partial | 1.162 | 0.923 | 1.260 | 1.084 | 1.000000 |
| B1_sad_derived | 1.475 | 0.792 | 1.862 | 1.262 | 1.000000 |
| B2_sad_precomputed | 1.481 | 1.018 | 1.454 | 0.982 | 1.000977 |
| C1_bitplane_parallel | 1.951 | 0.853 | 2.287 | 1.173 | 1.000000 |
| C2_bitplane_serial | 0.492 | 0.140 | 3.509 | 1.784 | 1.000000 |
| D1_lut_full | 1.430 | 1.115 | 1.283 | 0.897 | 1.000000 |
| D2_lut_segmented | 1.366 | 0.944 | 1.446 | 1.059 | 1.000000 |
| E1_booth | 0.930 | 0.978 | 0.951 | 1.023 | 1.000000 |
| E2_csa | 1.025 | 1.000 | 1.025 | 1.000 | 1.000000 |

### LANES = 32

| Architecture | LANES | Area um2 | Fmax* MHz | Cycles/dot | Dots/s* | Interactions/s* | Area @ matched throughput* | Metadata bits/row | Exact? |
|---|---:|---:|---:|---:|---:|---:|---:|---:|---|
| A1_mac_tree | 32 | 65176.3 | 202.29 | 128 | 1580419 | 6.473e+09 | 65176.3 | 0 | Yes, tested |
| A2_mac_partial | 32 | 77438.0 | 190.24 | 128 | 1486289 | 6.088e+09 | 82342.3 | 0 | Yes, tested |
| B1_sad_derived | 32 | 97270.8 | 151.95 | 128 | 1187072 | 4.862e+09 | 129502.3 | 0 | Yes, tested |
| B2_sad_precomputed | 32 | 93865.0 | 207.88 | 128 | 1624055 | 6.652e+09 | 91343.0 | 16 | Yes, tested |
| C1_bitplane_parallel | 32 | 122807.8 | 177.08 | 128 | 1383461 | 5.667e+09 | 140291.5 | 0 | Yes, tested |
| C2_bitplane_serial | 32 | 28143.2 | 105.72 | 512 | 206490 | 8.458e+08 | 215401.2 | 0 | Yes, tested |
| D1_lut_full | 32 | 93802.5 | 177.41 | 128 | 1385996 | 5.677e+09 | 106960.7 | 0 | Yes, tested |
| D2_lut_segmented | 32 | 90315.4 | 187.97 | 128 | 1468501 | 6.015e+09 | 97198.5 | 0 | Yes, tested |
| E1_booth | 32 | 60614.4 | 202.80 | 128 | 1584355 | 6.49e+09 | 60463.8 | 0 | Yes, tested |
| E2_csa | 32 | 66905.4 | 209.60 | 128 | 1637525 | 6.707e+09 | 64572.2 | 0 | Yes, tested |

| Architecture | Area ratio | Throughput ratio* | Area/throughput ratio* | Delay ratio | Storage ratio |
|---|---:|---:|---:|---:|---:|
| A1_mac_tree | 1.000 | 1.000 | 1.000 | 1.000 | 1.000000 |
| A2_mac_partial | 1.188 | 0.940 | 1.263 | 1.063 | 1.000000 |
| B1_sad_derived | 1.492 | 0.751 | 1.987 | 1.331 | 1.000000 |
| B2_sad_precomputed | 1.440 | 1.028 | 1.401 | 0.973 | 1.000977 |
| C1_bitplane_parallel | 1.884 | 0.875 | 2.152 | 1.142 | 1.000000 |
| C2_bitplane_serial | 0.432 | 0.131 | 3.305 | 1.913 | 1.000000 |
| D1_lut_full | 1.439 | 0.877 | 1.641 | 1.140 | 1.000000 |
| D2_lut_segmented | 1.386 | 0.929 | 1.491 | 1.076 | 1.000000 |
| E1_booth | 0.930 | 1.002 | 0.928 | 0.998 | 1.000000 |
| E2_csa | 1.027 | 1.036 | 0.991 | 0.965 | 1.000000 |

### LANES = 64

| Architecture | LANES | Area um2 | Fmax* MHz | Cycles/dot | Dots/s* | Interactions/s* | Area @ matched throughput* | Metadata bits/row | Exact? |
|---|---:|---:|---:|---:|---:|---:|---:|---:|---|
| A1_mac_tree | 64 | 128164.2 | 181.90 | 64 | 2842123 | 1.164e+10 | 128164.2 | 0 | Yes, tested |
| A2_mac_partial | 64 | 152204.7 | 187.64 | 64 | 2931817 | 1.201e+10 | 147548.3 | 0 | Yes, tested |
| B1_sad_derived | 64 | 192504.6 | 155.89 | 64 | 2435739 | 9.977e+09 | 224622.5 | 0 | Yes, tested |
| B2_sad_precomputed | 64 | 181454.0 | 172.20 | 64 | 2690653 | 1.102e+10 | 191669.0 | 16 | Yes, tested |
| C1_bitplane_parallel | 64 | 237242.5 | 161.57 | 64 | 2524596 | 1.034e+10 | 267081.4 | 0 | Yes, tested |
| C2_bitplane_serial | 64 | 51424.3 | 94.30 | 256 | 368360 | 1.509e+09 | 396770.0 | 0 | Yes, tested |
| D1_lut_full | 64 | 185444.1 | 182.14 | 64 | 2845876 | 1.166e+10 | 185199.6 | 0 | Yes, tested |
| D2_lut_segmented | 64 | 177948.2 | 183.22 | 64 | 2862807 | 1.173e+10 | 176662.5 | 0 | Yes, tested |
| E1_booth | 64 | 118951.6 | 188.42 | 64 | 2944053 | 1.206e+10 | 114833.2 | 0 | Yes, tested |
| E2_csa | 64 | 131273.4 | 201.95 | 64 | 3155425 | 1.292e+10 | 118239.3 | 0 | Yes, tested |

| Architecture | Area ratio | Throughput ratio* | Area/throughput ratio* | Delay ratio | Storage ratio |
|---|---:|---:|---:|---:|---:|
| A1_mac_tree | 1.000 | 1.000 | 1.000 | 1.000 | 1.000000 |
| A2_mac_partial | 1.188 | 1.032 | 1.151 | 0.969 | 1.000000 |
| B1_sad_derived | 1.502 | 0.857 | 1.753 | 1.167 | 1.000000 |
| B2_sad_precomputed | 1.416 | 0.947 | 1.495 | 1.056 | 1.000977 |
| C1_bitplane_parallel | 1.851 | 0.888 | 2.084 | 1.126 | 1.000000 |
| C2_bitplane_serial | 0.401 | 0.130 | 3.096 | 1.929 | 1.000000 |
| D1_lut_full | 1.447 | 1.001 | 1.445 | 0.999 | 1.000000 |
| D2_lut_segmented | 1.388 | 1.007 | 1.378 | 0.993 | 1.000000 |
| E1_booth | 0.928 | 1.036 | 0.896 | 0.965 | 1.000000 |
| E2_csa | 1.024 | 1.110 | 0.923 | 0.901 | 1.000000 |

### LANES = 128

| Architecture | LANES | Area um2 | Fmax* MHz | Cycles/dot | Dots/s* | Interactions/s* | Area @ matched throughput* | Metadata bits/row | Exact? |
|---|---:|---:|---:|---:|---:|---:|---:|---:|---|
| A1_mac_tree | 128 | 253822.2 | 177.64 | 32 | 5551164 | 2.274e+10 | 253822.2 | 0 | Yes, tested |
| A2_mac_partial | 128 | 299902.6 | 196.45 | 32 | 6138983 | 2.515e+10 | 271186.4 | 0 | Yes, tested |
| B1_sad_derived | 128 | 382724.6 | 167.89 | 32 | 5246669 | 2.149e+10 | 404936.3 | 0 | Yes, tested |
| B2_sad_precomputed | 128 | 356612.0 | 167.96 | 32 | 5248863 | 2.15e+10 | 377150.6 | 16 | Yes, tested |
| C1_bitplane_parallel | 128 | 465788.0 | 165.90 | 32 | 5184373 | 2.124e+10 | 498742.2 | 0 | Yes, tested |
| C2_bitplane_serial | 128 | 96533.8 | 82.72 | 128 | 646255 | 2.647e+09 | 829200.7 | 0 | Yes, tested |
| D1_lut_full | 128 | 369190.3 | 166.04 | 32 | 5188763 | 2.125e+10 | 394975.8 | 0 | Yes, tested |
| D2_lut_segmented | 128 | 354020.8 | 196.28 | 32 | 6133645 | 2.512e+10 | 320401.2 | 0 | Yes, tested |
| E1_booth | 128 | 235228.1 | 181.74 | 32 | 5679526 | 2.326e+10 | 229911.8 | 0 | Yes, tested |
| E2_csa | 128 | 260383.5 | 202.68 | 32 | 6333758 | 2.594e+10 | 228210.7 | 0 | Yes, tested |

| Architecture | Area ratio | Throughput ratio* | Area/throughput ratio* | Delay ratio | Storage ratio |
|---|---:|---:|---:|---:|---:|
| A1_mac_tree | 1.000 | 1.000 | 1.000 | 1.000 | 1.000000 |
| A2_mac_partial | 1.182 | 1.106 | 1.068 | 0.904 | 1.000000 |
| B1_sad_derived | 1.508 | 0.945 | 1.595 | 1.058 | 1.000000 |
| B2_sad_precomputed | 1.405 | 0.946 | 1.486 | 1.058 | 1.000977 |
| C1_bitplane_parallel | 1.835 | 0.934 | 1.965 | 1.071 | 1.000000 |
| C2_bitplane_serial | 0.380 | 0.116 | 3.267 | 2.147 | 1.000000 |
| D1_lut_full | 1.455 | 0.935 | 1.556 | 1.070 | 1.000000 |
| D2_lut_segmented | 1.395 | 1.105 | 1.262 | 0.905 | 1.000000 |
| E1_booth | 0.927 | 1.023 | 0.906 | 0.977 | 1.000000 |
| E2_csa | 1.026 | 1.141 | 0.899 | 0.876 | 1.000000 |

### LANES = 256

| Architecture | LANES | Area um2 | Fmax* MHz | Cycles/dot | Dots/s* | Interactions/s* | Area @ matched throughput* | Metadata bits/row | Exact? |
|---|---:|---:|---:|---:|---:|---:|---:|---:|---|
| A1_mac_tree | 256 | 504186.1 | 181.33 | 16 | 11333140 | 4.642e+10 | 504186.1 | 0 | Yes, tested |
| A2_mac_partial | 256 | 590201.0 | 185.84 | 16 | 11615287 | 4.758e+10 | 575864.5 | 0 | Yes, tested |
| B1_sad_derived | 256 | 763517.3 | 165.74 | 16 | 10358675 | 4.243e+10 | 835343.1 | 0 | Yes, tested |
| B2_sad_precomputed | 256 | 706583.9 | 158.24 | 16 | 9889898 | 4.051e+10 | 809696.4 | 16 | Yes, tested |
| C1_bitplane_parallel | 256 | 923433.1 | 151.76 | 16 | 9484801 | 3.885e+10 | 1103386.1 | 0 | Yes, tested |
| C2_bitplane_serial | 256 | 186049.7 | 74.79 | 64 | 1168556 | 4.786e+09 | 1804386.4 | 0 | Yes, tested |
| D2_lut_segmented | 256 | 705796.9 | 174.78 | 16 | 10923900 | 4.474e+10 | 732238.1 | 0 | Yes, tested |
| E1_booth | 256 | 468117.7 | 174.78 | 16 | 10923919 | 4.474e+10 | 485653.9 | 0 | Yes, tested |
| E2_csa | 256 | 518818.8 | 174.77 | 16 | 10923346 | 4.474e+10 | 538282.5 | 0 | Yes, tested |

| Architecture | Area ratio | Throughput ratio* | Area/throughput ratio* | Delay ratio | Storage ratio |
|---|---:|---:|---:|---:|---:|
| A1_mac_tree | 1.000 | 1.000 | 1.000 | 1.000 | 1.000000 |
| A2_mac_partial | 1.171 | 1.025 | 1.142 | 0.976 | 1.000000 |
| B1_sad_derived | 1.514 | 0.914 | 1.657 | 1.094 | 1.000000 |
| B2_sad_precomputed | 1.401 | 0.873 | 1.606 | 1.146 | 1.000977 |
| C1_bitplane_parallel | 1.832 | 0.837 | 2.188 | 1.195 | 1.000000 |
| C2_bitplane_serial | 0.369 | 0.103 | 3.579 | 2.425 | 1.000000 |
| D2_lut_segmented | 1.400 | 0.964 | 1.452 | 1.037 | 1.000000 |
| E1_booth | 0.928 | 0.964 | 0.963 | 1.037 | 1.000000 |
| E2_csa | 1.029 | 0.964 | 1.068 | 1.038 | 1.000000 |

## Target 500 MHz (2000 ps)

### LANES = 16

| Architecture | LANES | Area um2 | Fmax* MHz | Cycles/dot | Dots/s* | Interactions/s* | Area @ matched throughput* | Metadata bits/row | Exact? |
|---|---:|---:|---:|---:|---:|---:|---:|---:|---|
| A1_mac_tree | 16 | 33747.4 | 209.64 | 256 | 818910 | 3.354e+09 | 33747.4 | 0 | Yes, tested |
| A2_mac_partial | 16 | 39230.1 | 193.43 | 256 | 755567 | 3.095e+09 | 42519.0 | 0 | Yes, tested |
| B1_sad_derived | 16 | 49791.5 | 166.12 | 256 | 648895 | 2.658e+09 | 62837.2 | 0 | Yes, tested |
| B2_sad_precomputed | 16 | 49969.2 | 213.50 | 256 | 833970 | 3.416e+09 | 49066.8 | 16 | Yes, tested |
| C1_bitplane_parallel | 16 | 65828.1 | 178.79 | 256 | 698406 | 2.861e+09 | 77186.2 | 0 | Yes, tested |
| C2_bitplane_serial | 16 | 16592.2 | 117.50 | 1024 | 114745 | 4.7e+08 | 118415.1 | 0 | Yes, tested |
| D1_lut_full | 16 | 48255.0 | 233.70 | 256 | 912882 | 3.739e+09 | 43287.7 | 0 | Yes, tested |
| D2_lut_segmented | 16 | 46093.0 | 197.97 | 256 | 773320 | 3.168e+09 | 48810.3 | 0 | Yes, tested |
| E1_booth | 16 | 31382.6 | 204.94 | 256 | 800546 | 3.279e+09 | 32102.5 | 0 | Yes, tested |
| E2_csa | 16 | 34594.4 | 209.60 | 256 | 818733 | 3.354e+09 | 34601.9 | 0 | Yes, tested |

| Architecture | Area ratio | Throughput ratio* | Area/throughput ratio* | Delay ratio | Storage ratio |
|---|---:|---:|---:|---:|---:|
| A1_mac_tree | 1.000 | 1.000 | 1.000 | 1.000 | 1.000000 |
| A2_mac_partial | 1.162 | 0.923 | 1.260 | 1.084 | 1.000000 |
| B1_sad_derived | 1.475 | 0.792 | 1.862 | 1.262 | 1.000000 |
| B2_sad_precomputed | 1.481 | 1.018 | 1.454 | 0.982 | 1.000977 |
| C1_bitplane_parallel | 1.951 | 0.853 | 2.287 | 1.173 | 1.000000 |
| C2_bitplane_serial | 0.492 | 0.140 | 3.509 | 1.784 | 1.000000 |
| D1_lut_full | 1.430 | 1.115 | 1.283 | 0.897 | 1.000000 |
| D2_lut_segmented | 1.366 | 0.944 | 1.446 | 1.059 | 1.000000 |
| E1_booth | 0.930 | 0.978 | 0.951 | 1.023 | 1.000000 |
| E2_csa | 1.025 | 1.000 | 1.025 | 1.000 | 1.000000 |

### LANES = 32

| Architecture | LANES | Area um2 | Fmax* MHz | Cycles/dot | Dots/s* | Interactions/s* | Area @ matched throughput* | Metadata bits/row | Exact? |
|---|---:|---:|---:|---:|---:|---:|---:|---:|---|
| A1_mac_tree | 32 | 65176.3 | 202.29 | 128 | 1580419 | 6.473e+09 | 65176.3 | 0 | Yes, tested |
| A2_mac_partial | 32 | 77438.0 | 190.24 | 128 | 1486289 | 6.088e+09 | 82342.3 | 0 | Yes, tested |
| B1_sad_derived | 32 | 97270.8 | 151.95 | 128 | 1187072 | 4.862e+09 | 129502.3 | 0 | Yes, tested |
| B2_sad_precomputed | 32 | 93865.0 | 207.88 | 128 | 1624055 | 6.652e+09 | 91343.0 | 16 | Yes, tested |
| C1_bitplane_parallel | 32 | 122807.8 | 177.08 | 128 | 1383461 | 5.667e+09 | 140291.5 | 0 | Yes, tested |
| C2_bitplane_serial | 32 | 28143.2 | 105.72 | 512 | 206490 | 8.458e+08 | 215401.2 | 0 | Yes, tested |
| D1_lut_full | 32 | 93802.5 | 177.41 | 128 | 1385996 | 5.677e+09 | 106960.7 | 0 | Yes, tested |
| D2_lut_segmented | 32 | 90315.4 | 187.97 | 128 | 1468501 | 6.015e+09 | 97198.5 | 0 | Yes, tested |
| E1_booth | 32 | 60614.4 | 202.80 | 128 | 1584355 | 6.49e+09 | 60463.8 | 0 | Yes, tested |
| E2_csa | 32 | 66905.4 | 209.60 | 128 | 1637525 | 6.707e+09 | 64572.2 | 0 | Yes, tested |

| Architecture | Area ratio | Throughput ratio* | Area/throughput ratio* | Delay ratio | Storage ratio |
|---|---:|---:|---:|---:|---:|
| A1_mac_tree | 1.000 | 1.000 | 1.000 | 1.000 | 1.000000 |
| A2_mac_partial | 1.188 | 0.940 | 1.263 | 1.063 | 1.000000 |
| B1_sad_derived | 1.492 | 0.751 | 1.987 | 1.331 | 1.000000 |
| B2_sad_precomputed | 1.440 | 1.028 | 1.401 | 0.973 | 1.000977 |
| C1_bitplane_parallel | 1.884 | 0.875 | 2.152 | 1.142 | 1.000000 |
| C2_bitplane_serial | 0.432 | 0.131 | 3.305 | 1.913 | 1.000000 |
| D1_lut_full | 1.439 | 0.877 | 1.641 | 1.140 | 1.000000 |
| D2_lut_segmented | 1.386 | 0.929 | 1.491 | 1.076 | 1.000000 |
| E1_booth | 0.930 | 1.002 | 0.928 | 0.998 | 1.000000 |
| E2_csa | 1.027 | 1.036 | 0.991 | 0.965 | 1.000000 |

### LANES = 64

| Architecture | LANES | Area um2 | Fmax* MHz | Cycles/dot | Dots/s* | Interactions/s* | Area @ matched throughput* | Metadata bits/row | Exact? |
|---|---:|---:|---:|---:|---:|---:|---:|---:|---|
| A1_mac_tree | 64 | 128164.2 | 181.90 | 64 | 2842123 | 1.164e+10 | 128164.2 | 0 | Yes, tested |
| A2_mac_partial | 64 | 152204.7 | 187.64 | 64 | 2931817 | 1.201e+10 | 147548.3 | 0 | Yes, tested |
| B1_sad_derived | 64 | 192504.6 | 155.89 | 64 | 2435739 | 9.977e+09 | 224622.5 | 0 | Yes, tested |
| B2_sad_precomputed | 64 | 181454.0 | 172.20 | 64 | 2690653 | 1.102e+10 | 191669.0 | 16 | Yes, tested |
| C1_bitplane_parallel | 64 | 237242.5 | 161.57 | 64 | 2524596 | 1.034e+10 | 267081.4 | 0 | Yes, tested |
| C2_bitplane_serial | 64 | 51424.3 | 94.30 | 256 | 368360 | 1.509e+09 | 396770.0 | 0 | Yes, tested |
| D1_lut_full | 64 | 185444.1 | 182.14 | 64 | 2845876 | 1.166e+10 | 185199.6 | 0 | Yes, tested |
| D2_lut_segmented | 64 | 177948.2 | 183.22 | 64 | 2862807 | 1.173e+10 | 176662.5 | 0 | Yes, tested |
| E1_booth | 64 | 118951.6 | 188.42 | 64 | 2944053 | 1.206e+10 | 114833.2 | 0 | Yes, tested |
| E2_csa | 64 | 131273.4 | 201.95 | 64 | 3155425 | 1.292e+10 | 118239.3 | 0 | Yes, tested |

| Architecture | Area ratio | Throughput ratio* | Area/throughput ratio* | Delay ratio | Storage ratio |
|---|---:|---:|---:|---:|---:|
| A1_mac_tree | 1.000 | 1.000 | 1.000 | 1.000 | 1.000000 |
| A2_mac_partial | 1.188 | 1.032 | 1.151 | 0.969 | 1.000000 |
| B1_sad_derived | 1.502 | 0.857 | 1.753 | 1.167 | 1.000000 |
| B2_sad_precomputed | 1.416 | 0.947 | 1.495 | 1.056 | 1.000977 |
| C1_bitplane_parallel | 1.851 | 0.888 | 2.084 | 1.126 | 1.000000 |
| C2_bitplane_serial | 0.401 | 0.130 | 3.096 | 1.929 | 1.000000 |
| D1_lut_full | 1.447 | 1.001 | 1.445 | 0.999 | 1.000000 |
| D2_lut_segmented | 1.388 | 1.007 | 1.378 | 0.993 | 1.000000 |
| E1_booth | 0.928 | 1.036 | 0.896 | 0.965 | 1.000000 |
| E2_csa | 1.024 | 1.110 | 0.923 | 0.901 | 1.000000 |

### LANES = 128

| Architecture | LANES | Area um2 | Fmax* MHz | Cycles/dot | Dots/s* | Interactions/s* | Area @ matched throughput* | Metadata bits/row | Exact? |
|---|---:|---:|---:|---:|---:|---:|---:|---:|---|
| A1_mac_tree | 128 | 253822.2 | 177.64 | 32 | 5551164 | 2.274e+10 | 253822.2 | 0 | Yes, tested |
| A2_mac_partial | 128 | 299902.6 | 196.45 | 32 | 6138983 | 2.515e+10 | 271186.4 | 0 | Yes, tested |
| B1_sad_derived | 128 | 382724.6 | 167.89 | 32 | 5246669 | 2.149e+10 | 404936.3 | 0 | Yes, tested |
| B2_sad_precomputed | 128 | 356612.0 | 167.96 | 32 | 5248863 | 2.15e+10 | 377150.6 | 16 | Yes, tested |
| C1_bitplane_parallel | 128 | 465788.0 | 165.90 | 32 | 5184373 | 2.124e+10 | 498742.2 | 0 | Yes, tested |
| C2_bitplane_serial | 128 | 96533.8 | 82.72 | 128 | 646255 | 2.647e+09 | 829200.7 | 0 | Yes, tested |
| D1_lut_full | 128 | 369190.3 | 166.04 | 32 | 5188763 | 2.125e+10 | 394975.8 | 0 | Yes, tested |
| D2_lut_segmented | 128 | 354020.8 | 196.28 | 32 | 6133645 | 2.512e+10 | 320401.2 | 0 | Yes, tested |
| E1_booth | 128 | 235228.1 | 181.74 | 32 | 5679526 | 2.326e+10 | 229911.8 | 0 | Yes, tested |
| E2_csa | 128 | 260383.5 | 202.68 | 32 | 6333758 | 2.594e+10 | 228210.7 | 0 | Yes, tested |

| Architecture | Area ratio | Throughput ratio* | Area/throughput ratio* | Delay ratio | Storage ratio |
|---|---:|---:|---:|---:|---:|
| A1_mac_tree | 1.000 | 1.000 | 1.000 | 1.000 | 1.000000 |
| A2_mac_partial | 1.182 | 1.106 | 1.068 | 0.904 | 1.000000 |
| B1_sad_derived | 1.508 | 0.945 | 1.595 | 1.058 | 1.000000 |
| B2_sad_precomputed | 1.405 | 0.946 | 1.486 | 1.058 | 1.000977 |
| C1_bitplane_parallel | 1.835 | 0.934 | 1.965 | 1.071 | 1.000000 |
| C2_bitplane_serial | 0.380 | 0.116 | 3.267 | 2.147 | 1.000000 |
| D1_lut_full | 1.455 | 0.935 | 1.556 | 1.070 | 1.000000 |
| D2_lut_segmented | 1.395 | 1.105 | 1.262 | 0.905 | 1.000000 |
| E1_booth | 0.927 | 1.023 | 0.906 | 0.977 | 1.000000 |
| E2_csa | 1.026 | 1.141 | 0.899 | 0.876 | 1.000000 |

### LANES = 256

| Architecture | LANES | Area um2 | Fmax* MHz | Cycles/dot | Dots/s* | Interactions/s* | Area @ matched throughput* | Metadata bits/row | Exact? |
|---|---:|---:|---:|---:|---:|---:|---:|---:|---|
| A1_mac_tree | 256 | 504186.1 | 181.33 | 16 | 11333140 | 4.642e+10 | 504186.1 | 0 | Yes, tested |
| A2_mac_partial | 256 | 590201.0 | 185.84 | 16 | 11615287 | 4.758e+10 | 575864.5 | 0 | Yes, tested |
| B1_sad_derived | 256 | 763517.3 | 165.74 | 16 | 10358675 | 4.243e+10 | 835343.1 | 0 | Yes, tested |
| B2_sad_precomputed | 256 | 706583.9 | 158.24 | 16 | 9889898 | 4.051e+10 | 809696.4 | 16 | Yes, tested |
| C1_bitplane_parallel | 256 | 923433.1 | 151.76 | 16 | 9484801 | 3.885e+10 | 1103386.1 | 0 | Yes, tested |
| C2_bitplane_serial | 256 | 186049.7 | 74.79 | 64 | 1168556 | 4.786e+09 | 1804386.4 | 0 | Yes, tested |
| D2_lut_segmented | 256 | 705796.9 | 174.78 | 16 | 10923900 | 4.474e+10 | 732238.1 | 0 | Yes, tested |
| E1_booth | 256 | 468117.7 | 174.78 | 16 | 10923919 | 4.474e+10 | 485653.9 | 0 | Yes, tested |
| E2_csa | 256 | 518818.8 | 174.77 | 16 | 10923346 | 4.474e+10 | 538282.5 | 0 | Yes, tested |

| Architecture | Area ratio | Throughput ratio* | Area/throughput ratio* | Delay ratio | Storage ratio |
|---|---:|---:|---:|---:|---:|
| A1_mac_tree | 1.000 | 1.000 | 1.000 | 1.000 | 1.000000 |
| A2_mac_partial | 1.171 | 1.025 | 1.142 | 0.976 | 1.000000 |
| B1_sad_derived | 1.514 | 0.914 | 1.657 | 1.094 | 1.000000 |
| B2_sad_precomputed | 1.401 | 0.873 | 1.606 | 1.146 | 1.000977 |
| C1_bitplane_parallel | 1.832 | 0.837 | 2.188 | 1.195 | 1.000000 |
| C2_bitplane_serial | 0.369 | 0.103 | 3.579 | 2.425 | 1.000000 |
| D2_lut_segmented | 1.400 | 0.964 | 1.452 | 1.037 | 1.000000 |
| E1_booth | 0.928 | 0.964 | 0.963 | 1.037 | 1.000000 |
| E2_csa | 1.029 | 0.964 | 1.068 | 1.038 | 1.000000 |

