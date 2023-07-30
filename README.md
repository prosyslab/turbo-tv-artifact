# Translation Validation for JIT Compiler in the V8 JavaScript Engine (Paper Artifact)

This is the artifact of the paper Translation Validation for JIT Compiler in the V8 JavaScript Engine to appear in ICSE 2024.

## 1. Getting started

### System requirements

To run the experiments in the paper, we used a 64-core (Intel Xeon Processor Gold 6226R, 2.90 GHz) machine
with 512 GB of RAM and Ubuntu 22.04. We recommend running the experiments with at least 16-core machine with 32 GB of RAM.

### Loading Docker image

We provide the artifact as a Docker image. To launch the BayeSmith Docker image, run the following commands:

```bash
docker pull prosyslab/turbo-tv
docker run -it prosyslab/turbo-tv
```

It takes about [TODO] minutes to load the image.

### Notice

Most of the experiments take a long time. For convenience, all the data obtained from the instructions below are already shipped
in the Docker image. Also, we report the approximated running time of each instruction.

---

## 2. Directory structure [TODO]

```plaintext
├─ README.md                         <- The top-level README (this file)
│
└─ turbo-tv-exp                      <- Main implementation   │
   ├─ turbo-tv
   │   └─
   ├─ exp                            <- Script for experiment
   │
   ├─ benchmarks                     <- Benchmarks
   │  ├─ bug
   │  ├─ unit-js
   │  ├─ corpus
   │  └─ unit-llvm
   ...

```

---

## 3. Reproduce evaluation results

### 3.1 Effectiveness of TurboTV in discovering known bugs (Table 1)

### 3.2 Cumulative distribution of the validation time on the Corpus Benchmark (Figure 6)

### 3.3 Effectiveness of TurboTV for a large set of JS programs (Table 2)

### 3.4 Effectiveness of cross-language TV (Table 3)

### 3.5 Overhead of Fuzzilli combined with TurboTV (Figure 8)
