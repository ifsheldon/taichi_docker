# This is the image for running Taichi on CUDA & Vulkan backends
# cuda: 11.4
# vulkan 1.2.133
# build command: docker build . -t ifsheldon/vulkan-cuda-torch-taichi  .
# NOTE: building takes ~8min, size ~10G
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

RUN /bin/bash -c "cd /root && \
    source .bashrc && \
    python -m pip install taichi"