# ROCm Docker images
While you can obtain ROCm docker images from the [official ROCm Dockerhub registry](https://hub.docker.com/u/rocm), you may want to build them yourself. You have your reasons and I don't care what they are; I'm just glad you're here. Why is this repository here ? I have my reasons.

## Available container recipes
This repository contains Dockerfile recipes for creating container images built on various operating systems. 

* [Centos 8](./Dockerfile.centos8)
* [Ubuntu 22.04](./Dockerfile.ubuntu2204)

## Building it yourself
To build your docker images, you of course need [Docker installed](https://docs.docker.com/engine/install/). [The maintainers of this simple repository](https://www.fluidnumerics.com) will not help you install Docker; unless you are a paying customer (Come on! we gave you this free open-source repository).

Each container recipe has the following build arguments

* `ROCM_VERSION` - The version of ROCm you want to install in the container image. Can't find a single page with a complete list of ROCm versions ? Don't worry, we couldn't either. Just start with the default of `5.6` if you don't know what you're doing. If you know what you're doing, pick your favorite ROCm version.

* `PACKAGE_SET` - The set of ROCm packages to install. These refer to the packages that are managed by the operating system for ROCm. By default, this is set to `rocm-dev`. Couldn't find a single page with a complete list of ROCm packages available through package managers ? Don't worry, we couldn't either. Below, however, we've pulled a complete list for ROCm 5.6 . These packages may (or may not) be available with earlier (or later) versions of ROCm. In most cases, `rocm-dev` is available and will do just fine. Also, we don't recommend using ROCm version before 5.6, but alas, you may have your reasons.


To build on CentOS 8

```
docker build . --build-args ROCM_VERSION=5.6 --build-args PACKAGE_SET=rocm-dev -f Dockerfile.centos8 -t rocm5.6_centos8:latest
```

To build on Ubuntu 22.04

```
docker build . --build-args ROCM_VERSION=5.6 --build-args PACKAGE_SET=rocm-dev -f Dockerfile.ubuntu2204 -t rocm5.6_ubuntu2204:latest
```

## Getting the docker image size

```
docker inspect -f "{{ .Size }}" IMAGE
```

| Operating System | ROCm Version | Package set  | Size      |
| :--------------: | :----------: | :----------: |:--------: |
|   ubuntu 22.04   | rocm 5.6     | rocm-dev     | 5.726 GB  |
|     centos 8     | rocm 5.6     | rocm-dev     | 5.184 GB  |


## ROCm Packages

If you're interested in generating a package list for ROCm, you  can add the following line to your Docker recipe file

* [Centos 8](./Dockerfile.centos8) `RUN dnf search rocm`
* [Ubuntu 22.04](./Dockerfile.ubuntu2204) `RUN apt-cache search rocm`

In case you need a quick reference list of packages, below is a list of packages for ROCm (as of ROCm 5.6.0). 

* comgr - Library to provide support functions for ROCm code objects.
* hipfft-dev - ROCm FFT marshalling library
* hipfft - ROCm FFT marshalling library
* hsa-rocr - AMD Heterogeneous System Architecture HSA - Linux HSA Runtime for Boltzmann (ROCm) platforms
* rccl-dev - ROCm Communication Collectives Library
* rccl - ROCm Communication Collectives Library
* rocblas-dev - rocBLAS is AMD's library for BLAS on ROCm. It is implemented in HIP and optimized for AMD GPUs.
* rocblas - rocBLAS is AMD's library for BLAS on ROCm. It is implemented in HIP and optimized for AMD GPUs.
* rocfft-dev - ROCm FFT library
* rocfft - ROCm FFT library
* rocm-bandwidth-test - Diagnostic utility tool to measure PCIe bandwidth on ROCm platforms
* rocm-clang-ocl - OpenCL compilation with clang compiler.
* rocm-cmake - rocm-cmake built using CMake
* rocm-core - Radeon Open Compute (ROCm) Runtime software stack
* rocm-dbgapi - Library to provide AMD GPU debugger API
* rocm-debug-agent - Radeon Open Compute Debug Agent (ROCdebug-agent)
* rocm-dev - Radeon Open Compute (ROCm) Runtime software stack
* rocm-developer-tools - Radeon Open Compute (ROCm) Runtime software stack
* rocm-device-libs - Radeon Open Compute - device libraries
* rocm-gdb - ROCgdb
* rocm-hip-libraries - Radeon Open Compute (ROCm) Runtime software stack
* rocm-hip-runtime-dev - Radeon Open Compute (ROCm) Runtime software stack
* rocm-hip-runtime - Radeon Open Compute (ROCm) Runtime software stack
* rocm-hip-sdk - Radeon Open Compute (ROCm) Runtime software stack
* rocm-language-runtime - Radeon Open Compute (ROCm) Runtime software stack
* rocm-libs - Radeon Open Compute (ROCm) Runtime software stack
* rocm-llvm - ROCm compiler
* rocm-ml-libraries - Radeon Open Compute (ROCm) Runtime software stack
* rocm-ml-sdk - Radeon Open Compute (ROCm) Runtime software stack
* rocm-ocl-icd - clr built using CMake
* rocm-ocltst - clr built using CMake
* rocm-opencl-dev - clr built using CMake
* rocm-opencl-runtime - Radeon Open Compute (ROCm) Runtime software stack
* rocm-opencl-sdk - Radeon Open Compute (ROCm) Runtime software stack
* rocm-opencl - clr built using CMake
* rocm-openmp-sdk - Radeon Open Compute (ROCm) OpenMP Software development Kit.
* rocm-smi-lib - AMD System Management libraries
* rocm-utils - Radeon Open Compute (ROCm) Runtime software stack
* rocm-validation-suite - ROCm Validation Suite validates the AMD platform using ROCm Runtime - The ROCm Validation Suite is a system administrator and cluster manager's tool for detecting and troubleshooting common problems affecting AMD GPUs running in high performance computing environments, enabled using the ROCm software stack on a compatible platform.
* rocminfo - Radeon Open Compute (ROCm) Runtime rocminfo tool
* rocsolver-dev - AMD ROCm SOLVER library
