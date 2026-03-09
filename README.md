# Octopus: Efficient Hypergraph Pattern Mining with Practical Processing-in-Memory Architecture
## Project Overview

**Octopus** is an efficient hypergraph pattern mining (HPM) framework for the UPMEM **Processing-in-Memory (PIM)** architecture.

The goal of Octopus is to accelerate HPM tasks on large-scale hypergraphs using UPMEM DPUs. It integrates several system-level optimizations tailored for near-data processing architecture.

---

## 🚀 Key Features

- Fast hypergraph pattern mining for large-scale hypergraphs.
- Schedule-based compact data partitioning for collectively facilitate compact data organization.
- Load-aware balanced task assignment for balanced execution across thousands of DPUs.
- Hyperedge-level candidate generation for reduced computation.
- Asynchronous loader–worker pipeline using WRAM FIFO.

---

## 📁 Directory Structure

```
Octopus-AE/
├── data/         # Hypergraph data  
├── dpu/          # DPU-side programs (C for UPMEM)
├── host/         # Host-side logic (C)
├── include/      # Shared headers
├── makefile      # Compilation rules
└── README.md     # Project description
```

---

## 🛠 Requirements

- **Linux environment**
- **UPMEM SDK v2025.1.0.**
- **GNU Make, C compiler (e.g., `gcc`)**

## ⚙️ Build and Run Instructions

To run HPM on a hypergraph, use:

```bash
make clean
GRAPH=<hypergraph_name> PATTERN=<pattern_name> make test
```

Example:

```bash
GRAPH=SB PATTERN=HYP2_3_4_6 make test
```

> 💡 The available values for `GRAPH` and `PATTERN` are defined in `include/common.h`.  
> To add new hypergraphs or patterns, modify `common.h` and recompile.

## ⚡ Optimization Options

Octopus provides an optional optimization that uses the number of overlapping vertices between hyperedges as a pruning strategy. This optimization can be enabled or disabled through the `H2H` macro definition in `include/common.h` (line 86).

- **Default state**: The `H2H` macro is commented out (disabled by default)
- **To enable**: Uncomment line 86 in `include/common.h`:
  ```c
  #define H2H
  ```
- **To disable**: Comment out or remove the `H2H` definition:
  ```c
  //#define H2H
  ```

After modifying `common.h`, recompile the project for the changes to take effect.

## 📥 Download Hypergraph Data

```bash
pip install -r requirements.txt
python data/download.py
```

## 🙏 Acknowledgments

We gratefully acknowledge the foundational contributions of PimPam [SIGMOD'24], which inspired and informed much of this work.
We thank the authors for advancing the state of graph pattern mining on real Processing-in-Memory hardware and for generously releasing their implementation, which has been invaluable to our research.

Reference:
Shuangyu Cai, Boyu Tian, Huanchen Zhang, and Mingyu Gao. PimPam: Efficient Graph Pattern Matching on Real Processing-in-Memory Hardware. In Proceedings of the ACM on Management of Data (SIGMOD '24), Volume 2, Issue 3, Article 161, Pages 1–25.

---
