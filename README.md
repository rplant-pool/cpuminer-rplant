# cpuminer-rplant

A high-performance CPU miner for the [pool.rplant.xyz](https://pool.rplant.xyz) pool algorithms.

**Version 6.0.3b — BETA**

## What's new in 6.0.3b

- **The miner has been completely rebuilt** from the ground up.
- **No dev fee — 0%.** The miner mines only to your wallet.
- **Every pool CPU algorithm is now supported.**
- **Full support for multi-socket / multiprocessor systems.**
- **Major performance gains on most algorithms** — from +5% to +100% and beyond.
- **Automatic selection of the nearest working stratum.**
- **New algorithms:** neuromorph, rx/scash, rx/blockzero, rx/vrl (randomvirel), rx/0, rx/wow, xcrypt.
- **New build targets:** Linux arm64 and macOS arm64.

## Quick start

Ready-to-edit per-coin launch scripts are included (`miner-<coin>.sh` for Linux/macOS,
`miner-<coin>.bat` for Windows). Open one, set your wallet, and run it — or start the
miner manually:

```
cpuminer-rplant -a <algo> -o <port> -u <WALLET>.<worker>
```

## Pool URL (`-o`)

Several short forms are accepted. A **bare port** uses the geo picker, which automatically
connects to the nearest working stratum region:

```
-o <port>                              # geo — nearest region, plain
-o <port> --tls                        # geo — nearest region, TLS
-o eu.rplant.xyz:<port>                # fixed region, plain
-o eu.rplant.xyz:<port> --tls          # fixed region, TLS
-o stratum+tcp://eu.rplant.xyz:<port>  # explicit, plain
-o stratum+tcps://eu.rplant.xyz:<port> # explicit, TLS
```

Regions: `eu` (France), `asia` (Singapore), `na` (Canada).

## Threads (`-t`)

- `-t N` — use exactly **N** threads.
- `-t -N` — leave **N** threads free and use the rest (e.g. `-t -2` keeps 2 threads for the
  system). Handy to keep a machine responsive.
- omitted — automatic (default).

## CPU affinity (`--cpu-affinity`)

*TODO — a detailed description will be added later.*

## Options

```
Usage: cpuminer-rplant [OPTIONS]

  -a, --algo=ALGO           specify the algorithm to use
                              yespower       Ratatoskr
                              yespowertide   Tidecoin (TDC)
                              yespowerr16    Yenten (YTN)
                              yespowerurx    UraniumX (URX)
                              yespoweradvc   Adventurecoin (ADVC)
                              yespowermwc    Miners World Coin (MWC)
                              yespowersugar  Sugarchain (SUGAR)
                              yespoweriots   IOTS
                              yespower-b2b   generic yespower + blake2b
                              power2b        MicroBitcoin (MBC)
                              minotaurx      Avian (AVN)
                              yescrypt       Globalboost-Y (BSTY)
                              yescryptr8     BitZeny (ZNY)
                              yescryptr16    GoldCash (GOLD)
                              yescryptr32    LuckyPepe
                              gr             Raptoreum (RTM)
                              neuromorph     Cereblix (CRB)
                              rx/scash       SatoshiCash (SCASH)
                              rx/blockzero   BlockZero (BZR)
                              rx/byze        Byze (BYZ)
                              rx/vrl         Virel (VRL)
                              rx/0           Monero (XMR)
                              rx/wow         C64Chain
                              xcrypt         FlowCoin (FLX)
  -o, --url=URL             URL of mining server
  -u, --user=USERNAME       username for mining server
  -p, --pass=PASSWORD       password for mining server

      --bench=N[m]          run offline benchmark for N seconds (N minutes with m)
      --calibrate           measure the optimal thread count and exit
  -c, --config=FILE         load a JSON-format configuration file
      --cpu-affinity=MASK   pin threads to specific CPUs (advanced; TODO: detailed docs)
      --fullpower           slightly higher hashrate, but the machine becomes unresponsive
      --cpu-priority=N      set process priority (0 idle, 2 normal to 5 highest)
  -D, --debug               enable debug output
  -h, --help                display this help and exit
  -k, --keepalive           send keepalive to prevent timeout
  -l, --log-file=FILE       log all output to a file
      --msr=on|off          enable or disable the MSR mod for maximum hashrate (default: on)
      --noauto              disable geo stratum pick (use the given host only)
      --save                save the resulting config to file (autosave is off by default)
  -S, --rsyslog=HOST[:PORT] send log to a remote syslog server over UDP (default port 514)
      --reset-on-stale[=N]  reconnect after N stale shares in a row (default 3)
      --no-color            disable colored output
  -K, --param-key=KEY       key (pers) parameter for algos that use it
  -N, --param-n=N           N parameter for yespower/yescrypt algos
  -R, --param-r=N           R parameter for yespower/yescrypt algos
  -P, --protocol-dump       verbose dump of protocol-level activities
  -x, --proxy=HOST[:PORT]   connect through a SOCKS5 proxy (SOCKS5 only for now)
  -r, --retries=N           number of times to retry before switch to backup server (default: 5)
      --retry-pause=N       time to pause between retries, in seconds (default: 5)
  -t, --threads=N           CPU threads (default: auto; negative = leave that many threads free)
      --time-limit=N        maximum time [s] to mine before exiting the program
      --tls                 enable SSL/TLS support
      --user-agent=UA       set a custom user-agent string for the pool
  -V, --version             output version information and exit
```

## Supported coins

| Coin                    | Algo (-a)    | Port (-o) |
|-------------------------|--------------|-----------|
| Adventurecoin (ADVC)    | yespoweradvc | 7149      |
| Avian (AVN)             | minotaurx    | 7068      |
| Babacoin (BBC)          | gr           | 7082      |
| Bitmonero               | rx/0         | 7139      |
| BlockZero (BZR)         | rx/blockzero | 7170      |
| C64Chain                | rx/wow       | 7162      |
| Cascoin (CAS)           | minotaurx    | 7018      |
| Cereblix (CRB)          | neuromorph   | 7166      |
| FlowCoin (FLX)          | xcrypt       | 7173      |
| GoldCash (GOLD)         | yescryptr16  | 7048      |
| LiteDAG / Virel (VRL)   | rx/vrl       | 7152      |
| LuckyPepe               | yescryptr32  | 7047      |
| MicroBitcoin (MBC)      | power2b      | 7022      |
| Miners World Coin (MWC) | yespowermwc  | 7046      |
| Monero (XMR)            | rx/0         | 7080      |
| Obidoge                 | minotaurx    | 7063      |
| Raptoreum (RTM)         | gr           | 7056      |
| Ratatoskr               | yespower     | 7122      |
| Rhino                   | yespowerr16  | 7161      |
| Salvium (SAL)           | rx/0         | 7130      |
| SatoshiCash (SCASH)     | rx/scash     | 7019      |
| Tidecoin (TDC)          | yespowertide | 7059      |
| Yenten (YTN)            | yespowerr16  | 3382      |
| Zephyr (ZEPH)           | rx/0         | 7100      |

## Notes

- For best RandomX / heavy-algo performance, run as root/Administrator so the miner can
  apply the MSR mod (on by default) and use huge pages.
- Downloads: **Linux** x64 / arm64, **Windows** x64, **macOS** x64 / arm64, and a **HiveOS**
  custom-miner package.
