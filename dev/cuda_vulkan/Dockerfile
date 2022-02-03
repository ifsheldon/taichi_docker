# This is the image for developing/building Taichi with CUDA & Vulkan backends
# cuda: 11.4
# vulkan 1.2.133
# build command: docker build . -t ifsheldon/vulkan-cuda-torch-taichi-dev  .
# NOTE: building takes ~8min, size ~12G
# run command: docker run -it --rm --cpus=CPU_NUM --gpus all ifsheldon/vulkan-cuda-torch-taichi
# verify: 
# python 
# - import torch 
# - torch.ones(1).cuda() 
# - import taichi as ti 
# - ti.init(ti.vulkan) 
# - ti.init(ti.cuda)


FROM nvidia/vulkan:1.2.133-450
ENV PATH=/root/miniconda3/bin:${PATH} 

RUN cd /root && \
    wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -O ./miniconda.sh && \
    bash ./miniconda.sh  -b && \
    rm ./miniconda.sh  && \ 
    conda install -y mamba -c conda-forge && \
    mamba install -y pytorch cudatoolkit=11.3 -c pytorch && \
    mamba install -y numpy && \
    conda init bash

RUN cd /root && \
    apt update && \
    apt --yes install clang-10 unzip git build-essential cmake libxinerama-dev libxcursor-dev libxi-dev zlib1g-dev && \
    wget https://github.com/taichi-dev/taichi_assets/releases/download/llvm10_linux_patch2/taichi-llvm-10.0.0-linux.zip &&\
    unzip taichi-llvm-10.0.0-linux.zip -d llvm10ti && \
    rm ./taichi-llvm-10.0.0-linux.zip && \
    echo "export PATH=/root/llvm10ti/bin:\$PATH" >>  ./.bashrc
    
RUN /bin/bash -c "cd /root && \
    source .bashrc && \
    git clone --recursive https://github.com/taichi-dev/taichi && \
    cd taichi && \
    python -m pip install taichi && \
    python -m pip install --user -r requirements_dev.txt"

# RUN apt install vim