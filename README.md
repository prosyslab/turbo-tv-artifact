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