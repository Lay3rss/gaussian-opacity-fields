# Installation of Gaussian Binary Fields: Efficient and Compact Surface Reconstruction in Unbounded Scenes
- paper: https://arxiv.org/pdf/2404.10772
- project: https://github.com/autonomousvision/gaussian-opacity-fields

```
git clone https://github.com/autonomousvision/gaussian-opacity-fields.git
cd gaussian-opacity-fields

conda create -y -n gof python=3.8
conda activate gof

conda install pytorch torchvision torchaudio pytorch-cuda=11.8 -c pytorch -c nvidia
export CUDA_HOME=/usr/local/cuda-11.8

pip install -r requirements.txt

pip install submodules/diff-gaussian-rasterization
pip install submodules/simple-knn/

# tetra-nerf for triangulation
cd submodules/tetra-triangulation
conda install cmake
conda install conda-forge::gmp
conda install conda-forge::cgal

export LD_LIBRARY_PATH="/usr/local/cuda-11.8/lib64:$LD_LIBRARY_PATH"
export PATH=/usr/local/cuda-11.8/bin:$PATH
export CPATH=/usr/local/cuda-11.8/targets/x86_64-linux/include:$CPATH
export CMAKE_CUDA_ARCHITECTURES=native
cmake .
make
pip install -e .
```

if problem:
- remove the build
`rm -rf CMakeCache.txt CMakeFiles/`
- export all above variables
- relaunch `cmake .`

- references for cmake problems:
    - https://stackoverflow.com/questions/77727689/cmake-error-cmake-cuda-architectures-must-be-non-empty-if-set
    - https://github.com/abetlen/llama-cpp-python/issues/627
    - https://github.com/NVlabs/instant-ngp/issues/747
    - https://github.com/autonomousvision/gaussian-opacity-fields/issues/26

in CMakeLists.txt, add

set(CMAKE_CUDA_ARCHITECTURES 70 75 80)
set(CMAKE_CUDA_COMPILER /usr/local/cuda-11.8/bin/nvcc)
set(CUDACXX /usr/local/cuda-11.8/bin/nvcc)
