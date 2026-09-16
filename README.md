# clone-lin-bitcoin-core-nbits

Experimental LIN clone of Bitcoin Core v27.1 **CalculateNextWorkRequired** (compact nBits difficulty retarget). This repository is the LIN copy.

Results and the machine-written proof harness live in [kbelludoo/lin-open](https://github.com/kbelludoo/lin-open) (`examples/bitcoin_nbits/`, `test/prove_bitcoin_nbits_external.py`).

## Upstream

- Repo: [bitcoin/bitcoin](https://github.com/bitcoin/bitcoin)
- Tag: `v27.1` commit `1088a98f5aad080cc6cca2da174f206509fcda6c`
- License: **MIT**
- `src/pow.cpp` sha256 `a997ebc9e89ec0ed0f98fe56e7ece7c0a799746d36be5c0951ca6fd264280a33` blob `1e8d53de8bb87b0b9a30ff6439881cc2c40e38a4`
- `src/arith_uint256.cpp` sha256 `b46d67db26cef11a9da125b98e29bd8bf77b7a5c71418ee63bb77a0125a09d06` blob `0d5b3d5b0e6476b88053bd74a35c5cdbef1d2ae8`
- `src/test/pow_tests.cpp` sha256 `5911e49b195af6dac2e4e94f5509537555172ae9c6a4816dc06c147cd8c6d0ae` blob `3a44d1da499852cbdf6206bbf5026a50a9610f2f`

## Canonical vectors (pow_tests.cpp)

| case | last nBits | expected |
|---|---|---|
| get_next_work | `0x1d00ffff` | `0x1d00d86a` |
| pow_limit | `0x1d00ffff` | `0x1d00ffff` |
| lower_limit | `0x1c05a3f4` | `0x1c0168fd` |
| upper_limit | `0x1c387f6f` | `0x1d00e1fd` |

Class: **EXPERIMENTAL**. Not a Bitcoin node. Not SHA256d CheckProofOfWork.

## Reproduce (C11 oracle, no Zig)

```
gcc -O2 -std=c11 -o bitcoin_nbits_c11 test/oracles/bitcoin_nbits_c11.c
./bitcoin_nbits_c11 selftest
./bitcoin_nbits_c11 next 0x1d00ffff 1262152739 1261130161
```
