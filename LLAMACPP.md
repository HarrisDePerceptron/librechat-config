
Cuda toolkit install:

make sure you have the cuda_toolkit install.
check by 
nvcc --verison

if this does not exists then install it. make sure cuda toolkit and driver cuda mathces.

First check which cuda version the nvidia driver is build against:
nvidia-smi
this will display the cuda version. now select th appropriate cuda version from the list.
the version should be exact 12.8 != 12.8.1

https://developer.nvidia.com/cuda-toolkit-archive


After installation make sure cuda is in the path 
#bashrc or bash_aliases

export PATH=/usr/local/cuda/bin:$PATH
export LD_LIBRARY_PATH=/usr/local/cuda/lib64


Restart terminal 

# Cuda compute capability lookup: https://developer.nvidia.com/cuda-gpus
# RTX 3090 = 8.6 compute capability
# 8.6 = CMAKE_CUDA_ARCHITECTURES="86"





rm -rf build CMakeCache.txt
    
 cmake -B build \
  -DGGML_CUDA=ON \
  -DCMAKE_BUILD_TYPE=Release \
  -DBUILD_SHARED_LIBS=OFF \
  -DLLAMA_CURL=ON \
  -DCMAKE_CUDA_ARCHITECTURES="86" # Compute capbility lookup for your gpu
  
  
cmake \
	--build build \
	--config Release \
	-j8 \
	--clean-first
	

cd build/bin/


./llama-cli \
    -hf unsloth/Qwen3-Coder-30B-A3B-Instruct-GGUF:Q4_K_XL \
    --jinja -ngl 99 --threads -1 --ctx-size 32684 \
    --temp 0.7 --min-p 0.0 --top-p 0.80 --top-k 20 --repeat-penalty 1.05
    
    
## Llama Server


./llama-server \
  -hf unsloth/Qwen3-Coder-30B-A3B-Instruct-GGUF:Q4_K_XL \
  --jinja \
  --n-gpu-layers 99 \
  --threads -1 \
  --ctx-size 32684 \
  --temp 0.7 \
  --min-p 0.0 \
  --top-p 0.80 \
  --top-k 20 \
  --repeat-penalty 1.05 \
  --host 0.0.0.0 \
  --port 8080
