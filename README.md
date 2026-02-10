# CPU Benchmark for Mikrotik Devices with container support

## RouterOS Device Results
| Device                  | CPU             | RouterOS Version |  CPU Core | int64 (1 Thread) | matrixprod (1 Thread) | int64 (ALL Threads) ↓ | matrixprod (ALL Threads) |
|-------------------------|-----------------|-----------------|--------------|----------------|---------------------|-------------------|------------------------|
| CCR2116-12G-4S+ | AL73400 | arm64 | 16                      | 919.58        | 31.76             | 13739.46           | 469.58                |
| x86 router Beelink mini S13 | intel N150 | x86 | 4                      | 1690.67        | 2735.50             | 5459.61           | 4571.61                |
| x86 router | intel N100 | x86 | 4                      | 1587.47        | 2442.24             | 4134.63           | 4317.04                |
| RB5009UG+S | 88F7040 | arm64 | 4                         | 640.61         | 22.09               | 2562.37           | 86.60                  |
| H53UiG-5HaxQ2HaxQ (Chateau PRO ax) | IPQ-8072A | arm64 |4| 560.27         | 22.38               | 2214.59           | 64.17                  |
| CCR2004-16G-2S+ | AL32400 | arm64 | 4                         | 542.37         | 18.44               | 2020.24           | 66.90                  |
| x86 router AZW Z83 II | Intel(R) Atom(TM) x5-Z8350 | x86 | 4                      | 533.77        | 322.83             | 1867.16           | 1125.30                |
| C53UiG+5HPaxD2HPaxD (hAP ax3) <br> cAP LTE12 ax| IPQ-6010 | arm64 | 4      | 455.11         | 18.84               | 1815.39           | 57.21                  |
| RB4011iGS+5HacQ2HnD | AL21400 | arm32 | 4              | 234.60         | 206.92               | 933.35            | 764.67                  |
| C52iG-5HaxD2HaxD-TC (hAP ax2)| IPQ-6010 | arm64 | 4      | 218.51         | 9.24                | 871.49            | 31.66                  |
| L009UiGS | IPQ-5018 | arm64  | 2      | 254.10         | 7.10              | 499.43            | 13.33                 |
| RBD52G-5HacD2HnD-TC (hAP ac2) | IPQ-4018 | arm32  | 4      | 102.80         | 110.87              | 409.78            | 185.74                 |
| RBD53iG-5HacD2HnD (hAP ac3) | IPQ-4019 | arm32  | 4      | 103.20         | 107.72              | 395.64            | 193.26                 |
| L41G (hAP ax lite) | IPQ-5010 | arm32 | 2                | 137.87         | 33.56               | 272.74            | 33.88                  |
| L009UiGS | IPQ-5018 | arm32  | 2      | 136.34         | 28.39              | 256.14            | 29.96                 |
| E60iUGS (hEX S 2025) | EN7562CT | armv5 | 2              | 113.14         | 21.39               | 225.71            | 37.92                  |
| CRS326-24G-2S+ | 98DX3236 | arm32 | 2                | 84.54         | 65.92               | 84.66            | 83.15                  |

## How run test?
```
/interface/veth add name=CPUTEST
/disk add type=tmpfs tmpfs-max-size=100M slot=RAM
/container/add remote-image=registry-1.docker.io/wiktorbgu/tools:cpu-bench interface=CPUTEST logging=yes check-certificate=no root-dir=/RAM/cputest
/container start [find interface=CPUTEST]
```
wait ~2 minutes and check container log!

> [!NOTE]
> RouterOS devices tested with [wiktorbgu/tools:cpu-bench](https://hub.docker.com/r/wiktorbgu/tools/tags) docker container based on alpine-minirootfs-3.22.1, stress-ng 0.18.0  
> x86 with RouterOS


# CPU Benchmark for OpenWrt Devices
This script benchmarks CPU performance on OpenWrt devices using stress-ng.

It measures **Bogo Ops/s** for **int64** and **matrixprod** methods on both single-thread and multi-thread execution.

The results are printed as a Markdown-formatted table row, ready to be copied into the table below.  
Feel free to submit a pull request with benchmark results from your device.

## Run
> [!NOTE]
> Tested only OpenWrt

```
sh <(wget -O - https://raw.githubusercontent.com/itdoginfo/cpu-wrt-bench/refs/heads/main/cpu-wrt-bench.sh)
```

## Device Results
| Device                  | CPU             | OpenWrt Version |  CPU Threads | int64 (1 Thread) | matrixprod (1 Thread) | int64 (ALL Threads) | matrixprod (ALL Threads) |
|-------------------------|-----------------|-----------------|--------------|----------------|---------------------|-------------------|------------------------|
| Beeline SmartBox TURBO+ | MediaTek MT7621A | OpenWrt 24.10.1 | 4           | 35.77          | 7.88                | 92.83             | 17.94                  |
| Xiaomi Mi Router AX3000T | MediaTek MT7981BA  | OpenWrt 24.10.1 | 2        | 291.67         | 10.89               | 581.33            | 19.86                  |
| FriendlyElec NanoPi R2S | Rockchip RK3328 | OpenWrt 24.10.1 | 4            | 286.60         | 10.80               | 1144.74           | 35.30                  |
| Xiaomi Redmi Router AX6000 | MediaTek MT7986A | OpenWrt 24.10.1 | 4        | 451.73         | 18.78               | 1805.96           | 55.30                  |

> [!NOTE]
> n/s - CPU not supported int128 method.
