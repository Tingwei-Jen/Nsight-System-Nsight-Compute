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
