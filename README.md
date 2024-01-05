# TurboTV Artifact

This is the artifact of the paper "Translation Validation for JIT Compiler in the V8 JavaScript Engine" to appear in ICSE 2024.
The paper presents [TurboTV](https://github.com/prosyslab/turbo-tv), the first SMT-based translation validation tool for the TurboFan engine of V8.

## System requirements

To run the experiments in the paper, we used a 64-core (Intel Xeon Processor Gold 6226R, 2.90 GHz) machine
with 512 GB of RAM and Ubuntu 22.04. We recommend running the experiments with at least a 16-core machine with 32 GB of RAM.

## Loading Docker image

We provide the artifact as a Docker image. To launch the Turbo-TV Docker image, run the following commands:

```bash
docker pull prosyslab/turbo-tv
docker run -it --privileged prosyslab/turbo-tv
```

The artifact implementation is at `/home/user/turbo-tv-exp`.

### Notice

Most of the experiments take a long time. For convenience, all the data obtained from the instructions below are already shipped in the Docker image.


## Directory Structure
```plaintext
├─ README.md                    <- This file
├─ turbo-tv                     <- Main implementation
├─ exp                          <- Script for experiments
├─ benchmarks                   <- Benchmarks
│  ├─ unit-js
│  ├─ corpus
│  ├─ unit-llvm
│  └─ ...
├─ fuzzilli                     <- Validation corpus generator implemented on Fuzzilli
├─ d8s                          <- d8 builds for each TurboFan bugs
│  ├─ 1126249
│  ├─ 1198705
│  └─ ...
├─ eval                         <- Evaluation results. Counterexamples list in here.
├─ workbenchs                   <- Workbenchs for reproduced evaluation. All the data is already in here.
│  ├─ workbench-corpus
│  ├─ workbench-unitjs
│  └─ ...
├─ issues                       <- Build configuration and PoC for each TurboFan bugs
```

## Usage
We provide a script for easy use of Turbo-TV. The script helps Turbo-TV to receive the js files and perform Translation Validation. The script works in a [pyenv](https://github.com/pyenv/pyenv) environment.
```bash
$ pyenv activate turbo-tv
(turbo-tv) $./exp v8 --select --issue 1199345                   # switch v8 for issue #1199345
(turbo-tv) $./exp turbo-tv --check-ub issues/1199345/1199345.js # Check UB
(turbo-tv) $./exp turbo-tv --check-eq issues/1199345/1199345.js # Check EQ
```

The EQ check output would be as follows:
```plaintext
====================[Check EQ of js(s) in target dir]====================
[1] Emit reductions
100%|██████████████████████████████████████████████| 1/1 [00:00<00:00,  4.40it/s]
[2] Check EQ
/home/user/turbo-tv-exp/workbench/1199345/1: O
/home/user/turbo-tv-exp/workbench/1199345/3: O
/home/user/turbo-tv-exp/workbench/1199345/4: O
/home/user/turbo-tv-exp/workbench/1199345/5: O
/home/user/turbo-tv-exp/workbench/1199345/8: O
/home/user/turbo-tv-exp/workbench/1199345/9: O
/home/user/turbo-tv-exp/workbench/1199345/10: O
/home/user/turbo-tv-exp/workbench/1199345/6: O
/home/user/turbo-tv-exp/workbench/1199345/7: O
/home/user/turbo-tv-exp/workbench/1199345/2: X
c.e. => /home/user/turbo-tv-exp/workbench/1199345/2.ce
100%|██████████████████████████████████████████████| 10/10 [00:01<00:00,  6.50it/s]
EQ check done. Elapsed(s): 1.5940730571746826
               Avg Elapsed(s): 0.15940730571746825
```

*c.e. => /home/user/turbo-tv-exp/workbench/1199345/2.ce* indicates that the counter-example is saved at `/home/user/turbo-tv-exp/workbench/1199345/2.ce`. You can find the following counter-example there.

```plaintext
Result: Not Verified
CounterExample:
Parameters:
Parameter[0]: TaggedSigned(0)
Parameter[1]: TaggedSigned(865386496)

State of src
#0:NumberConstant(0) [Range (0.000000, 0.000000)] =>
  Value: TaggedSigned(0)
  ControlToken: false
  UB: false
  Deopt: false
#1:NumberConstant(-0) [MinusZero] =>
  Value: Float64(-0.0)
  ControlToken: false
  UB: false
  Deopt: false
#2:Start() [Internal] =>
  Value: empty
  ControlToken: true
  UB: false
  Deopt: false
...
```


## Reproduce Evaluation
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

Effectiveness of cross-language TV for unit tests in [LLVM](https://github.com/llvm/llvm-project). (Table 2)
```bash
(turbo-tv) $./exp eval --cross-validation
```

**RQ3. Fuzzer Overhead**
The following command will augment and validate the corpus already been created.
```bash
./exp eval --overhead --corpus benchmarks/corpus-overhead/
```

For convenience, we provide a command to generate a corpus from scratch.
For example, the following command generates random JS files for 10 seconds and measures overhead on the generated corpus 
```bash
./exp eval --overhead --timeout 10
```


