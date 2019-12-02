#***************************************************
# Docker build pyrotch file for ARM processors
#***************************************************
FROM nvcr.io/nvidia/l4t-base:r32.2

RUN apt-get update && \
    apt-get install -y python3-pip libjpeg-dev zlib1g-dev

# install pytorch for Xavier AGX
ARG torchtmp=/torchtmp
RUN mkdir $torchtmp && cd $torchtmp && \
    wget https://nvidia.box.com/shared/static/phqe92v26cbhqjohwtvxorrwnmrnfx1o.whl -O torch-1.3.0-cp36-cp36m-linux_aarch64.whl && \
    pip3 install numpy torch-1.3.0-cp36-cp36m-linux_aarch64.whl

# other python packages
RUN pip3 install torchvision

RUN mkdir mat && cd mat && \
  wget https://files.pythonhosted.org/packages/75/81/53ccadcb8cad0a9837f1487b57f2b46b21caa2b3f35f72bc1acb06b5825c/matplotlib-3.1.2.tar.gz && tar xvf matplotlib-3.1.2.tar.gz

# create matplotlib from source
RUN apt-get install -y libfreetype6-dev
ENV CC=gcc CXX=g++ PKG_CONFIG=x86_64-pc-linux-gnu-pkg-config
RUN cd /mat/matplotlib-3.1.2 && python3 -mpip install .

# install jupyter
RUN python3 -m pip install --upgrade pip && python3 -m pip install jupyter
