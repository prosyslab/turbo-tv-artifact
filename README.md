# Translation Validation for JIT Compiler in the V8 JavaScript Engine (Paper Artifact)

This is the artifact of the paper Translation Validation for JIT Compiler in the V8 JavaScript Engine to appear in ICSE 2024.

## Getting started

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
