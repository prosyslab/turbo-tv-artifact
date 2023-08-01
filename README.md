# TurboTV Experiment

This is the artifact of the paper Translation Validation for JIT Compiler in the V8 JavaScript Engine to appear in ICSE 2024.

### System requirements

To run the experiments in the paper, we used a 64-core (Intel Xeon Processor Gold 6226R, 2.90 GHz) machine
with 512 GB of RAM and Ubuntu 22.04. We recommend running the experiments with at least 16-core machine with 32 GB of RAM.

### Loading Docker image

We provide the artifact as a Docker image. To launch the BayeSmith Docker image, run the following commands:

```bash
docker pull turbotv2024/turbo-tv
docker run -it turbotv2024/turbo-tv
```

It takes about [TODO] minutes to load the image.

The artifact implementation is at `/home/user/turbo-tv-exp`; you can find the detail at `README.md` in there.

### Notice

Most of the experiments take a long time. For convenience, all the data obtained from the instructions below are already shipped
in the Docker image. 


## Directory Structure
```plaintext
├─ README.md                    <- This file
├─ turbo-tv                     <- Main implementation
├─ exp                          <- Script for experiments
├─ benchmarks                   <- Benchmarks
│  ├─ unit-js
│  ├─ corpus
│  └─ unit-llvm
├─ d8s                          <- d8 builds for each TurboFan bugs
│  ├─ 1126249
│  ├─ 1198705
│  └─ ...
├─ eval                         <- Evaluation results. Counter Examples list in here.
├─ workbenchs                   <- Workbenchs for reproduced evaluation. All the data already in here.
│  ├─ workbench-corpus
│  ├─ workbench-unitjs
│  └─ ...
├─ issues                       <- Build configuration and PoC for each TurboFan bugs
├─ example                      <- Example javascriptsls
```

## Usage
We provide a script for easy use of Turbo-TV. The script helps Turbo-TV to receive the js files and perform Translation Validation. The script works in a [pyenv](https://github.com/pyenv/pyenv) environment.
```bash
$ pyenv activate turbo-tv
(turbo-tv) $./exp turbo-tv --check-eq example/add.js --timeout=10 # check EQ for one JS
(turbo-tv) $./exp turbo-tv --check-ub example/add.js --timeout=10 # check UB for one JS
(turbo-tv) $./exp turbo-tv --check-eq example --timeout=10        # validate JSs in the directory
```

## Reproduce Evaluation (Table 1, Table 2 and Table 3)
The following commands run Turbo-TV to reproduce experiments in the paper.

**RQ1. Precision and Scalability of TurboTV**

**Precision:** Effectiveness of TurboTV in discovering known bugs. (Table 1)
```bash
(turbo-tv) $./exp eval --precision
```

**Scalability:** Effectiveness of TurboTV for a large set of JS programs. (Table 2)
```bash
(turbo-tv) $./exp eval --scalability
```
**RQ2. Effectiveness of Cross-Language TV**

Effectiveness of cross-language TV for unit tests in [LLVM](https://github.com/llvm/llvm-project). (Table 3)
```bash
(turbo-tv) $./exp eval --cross-validation
```
