# Nsight_Compute_Tutorial

## Docker container

To build the Docker container, follow these steps:

1. Open a terminal and navigate to the `Nsight_Compute_Tutorial/docker` directory.
2. Run the following command to build the container without caching:

```bash
docker build -t cuda_nsight:v0.1 --no-cache --rm --file Dockerfile.nsight .
```

To run the Docker container, execute the following command:

```bash
cd Nsight_Compute_Tutorial
docker run -it --rm --gpus all --cap-add=SYS_ADMIN --volume="$PWD:/workspace" cuda_nsight:v0.1
```

Make sure to replace `cuda_nsight:v0.1` with the appropriate image name and version.


## How to use nvprof
基本命令  
  1. 簡單分析
  ```bash
  nvprof ./your_cuda_application
  ```
  2. 輸出到 .nvprof 文件, 可以通过 nvprof 或 nvvp 工具进行后续分析
  ```bash
  nvprof --output-profile my_profile.nvprof ./your_cuda_application
  ```
  3. 輸出到 .nvvp , 用于 NVIDIA Visual Profiler (nvvp) 中的可视化分析。
  ```bash
  nvprof --export-profile my_timeline_report.nvvp ./your_cuda_application
  ```

Event and Metrics  
  1. all events
  ```bash
  nvprof --events all ./your_cuda_application
  ```
  2. certain events.
  ```bash
  nvprof --events event1,event2 ./your_cuda_application
  ```
  3. certain metrics and 輸出到.nvvp
  ```bash
  nvprof --metrics metric1,metric2 --export-profile my_timeline_report.nvvp  ./your_cuda_application
  ```

## How to use Nsight system
### User guide
https://docs.nvidia.com/nsight-systems/UserGuide/index.html  

  1. 簡單分析
  ```bash
   nsys profile ./your_cuda_application
   nsys profile --stats=true ./your_cuda_application
  ```
  2. save report as my_profile
  ```bash
   nsys profile --stats=true -o my_profile ./your_cuda_application
   nsys profile --stats=true --trace=cuda -o my_profile ./your_cuda_application
   nsys profile --stats=true --trace=osrt,cuda,nvtx --show-output=true --output=my_profile ./your_cuda_application
  ```
## How to use Nsight compute
### User guide
https://docs.nvidia.com/nsight-compute/NsightCompute/index.html#
  1. save report as my_profile
  ```bash
  ncu --export=my_profile ./your_cuda_application
  ncu --target-processes=all --export=/workspace/report/sgemm --set=full --force-overwrite ./sgemm
  ```
  2. show profiling result in terminal
  ```bash
  ncu --import my_profile.ncu-rep --page=detail
  ```

### Facing problem: ERR_NVGPUCTRPERM: Permission issue with Performance Counters 
- Solution: add `--cap-add=SYS_ADMIN` in docker run.

## Remote Profiling on Windows Visual Profiler (Host)
  1. Download and install cuda-tool-kit with same version of device. https://developer.nvidia.com/cuda-11-8-0-download-archive
  2. Download JRE1.8 https://www.java.com/zh-TW/download/
  3. Search Visual Profiler in Host.

## Remote Profiling on Windows Nsight System and Compute (Host)
  1. Download and install cuda-tool-kit with same version of device. https://developer.nvidia.com/cuda-11-8-0-download-archive. Nsight system is included.
  2. Download JRE1.8 https://www.java.com/zh-TW/download/
  3. Download latest Nsignt Compute https://developer.nvidia.com/nsight-compute
  - In Device
    - install Nsight system https://docs.nvidia.com/nsight-systems/InstallationGuide/index.html
    - install Nsight compute https://developer.nvidia.com/blog/using-nsight-compute-in-containers/  

## Reference
[CUDA Profiler](https://docs.nvidia.com/cuda/profiler-users-guide/index.html#)  
[CUDA Programming Guild](https://docs.nvidia.com/cuda/cuda-c-programming-guide/index.html)  
[Learn-CUDA-Programming](https://github.com/PacktPublishing/Learn-CUDA-Programming?tab=readme-ov-file)  
[CUDA Parallel Reduction](https://developer.download.nvidia.com/assets/cuda/files/reduction.pdf)
