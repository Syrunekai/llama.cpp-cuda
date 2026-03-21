# llama.cpp CUDA Builds

Forked from [ai-dock/llama.cpp-cuda](https://github.com/ai-dock/llama.cpp-cuda). This version adds CUDA 13.2 support alongside the original CUDA 12.9 builds.

This repository automatically builds [llama.cpp](https://github.com/ggml-org/llama.cpp) with CUDA support for multiple NVIDIA GPU architectures and CUDA versions.

## Why This Repository?

The official llama.cpp repository does not provide pre-built CUDA binaries. This repository fills that gap by:

- Building llama.cpp with CUDA support for multiple CUDA toolkit versions
- Supporting a wide range of NVIDIA GPU architectures (compute capability 7.5+)
- Automatically tracking upstream llama.cpp releases
- Providing ready-to-use binaries via GitHub releases

## Supported Configurations

### CUDA Versions
- CUDA 12.9
- CUDA 13.2

### GPU Architectures

| Compute Capability | GPU Examples |
|-------------------|--------------|
| 7.5 | Tesla T4, RTX 2000 series, Quadro RTX |
| 8.0 | A100 |
| 8.6 | RTX 3000 series |
| 8.9 | RTX 4000 series, L4, L40 |
| 9.0 | H100, H200 |
| 10.0 | B200 |
| 12.0 | RTX Pro series, RTX 5000 series |

## Usage

### Download

1. Go to the [Releases](../../releases) page
2. Download the tarball for your CUDA version (e.g., `llama.cpp-bXXXX-cuda-13.2.tar.gz`)
3. Extract the archive:

```bash
tar -xzf llama.cpp-bXXXX-cuda-13.2.tar.gz
cd cuda-13.2
```

### Run

The extracted directory contains all llama.cpp binaries:

```bash
# Run the main CLI
./llama-cli --help

# Run the server
./llama-server --help

# Other utilities
./llama-bench
./llama-quantize
./llama-embedding
```

### Check Version

Each release includes a `VERSION.txt` file with build information:

```bash
cat VERSION.txt
```

## System Requirements

- NVIDIA GPU with compute capability 7.5 or higher
- Appropriate NVIDIA driver for your CUDA version:
  - CUDA 12.9: Driver >= 570.15
  - CUDA 13.2: Driver >= 580.00
- Linux x86_64 (Ubuntu 24.04 compatible)

## Build Process

Builds are triggered automatically:
- Daily at 00:00 UTC
- Only if a new llama.cpp release is detected
- Can be manually triggered via GitHub Actions

Each build:
1. Checks for new llama.cpp releases
2. Clones llama.cpp at the exact release commit
3. Builds with CMake using CUDA Docker images
4. Packages binaries for each CUDA version
5. Creates a GitHub release with all build artifacts

## Choosing Your CUDA Version

Select based on:
1. **Your GPU architecture** - Blackwell GPUs require CUDA 12.9+
2. **Your installed CUDA toolkit** - Match the version if possible
3. **Your NVIDIA driver** - Ensure your driver supports the CUDA version

## Manual Building

If you need a custom build:

```bash
git clone https://github.com/Syrunekai/llama.cpp-cuda
cd llama.cpp-cuda

# Edit .github/workflows/build-cuda.yml to customize architectures or CUDA versions
# Then trigger a manual workflow run
```

## License

This repository contains build scripts only. The llama.cpp binaries are subject to the [llama.cpp MIT License](https://github.com/ggml-org/llama.cpp/blob/master/LICENSE).

## Links

- **Upstream llama.cpp**: https://github.com/ggml-org/llama.cpp
- **Original build repo**: https://github.com/ai-dock/llama.cpp-cuda
- **CUDA Toolkit**: https://developer.nvidia.com/cuda-toolkit
- **NVIDIA Driver Downloads**: https://www.nvidia.com/download/index.aspx

## Credits

- [llama.cpp](https://github.com/ggml-org/llama.cpp) by Georgi Gerganov and contributors
- Original build pipeline by [ai-dock](https://github.com/ai-dock)
