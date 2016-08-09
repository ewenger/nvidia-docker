FROM cuda:7.5-runtime
MAINTAINER NVIDIA CORPORATION <digits@nvidia.com>

RUN apt-get update && apt-get install -y --no-install-recommends --force-yes \
        cuda-core-$CUDA_PKG_VERSION \
        cuda-misc-headers-$CUDA_PKG_VERSION \
        cuda-command-line-tools-$CUDA_PKG_VERSION \
        cuda-license-$CUDA_PKG_VERSION \
        cuda-nvrtc-dev-$CUDA_PKG_VERSION \
        cuda-cusolver-dev-$CUDA_PKG_VERSION \
        cuda-cublas-dev-$CUDA_PKG_VERSION \
        cuda-cufft-dev-$CUDA_PKG_VERSION \
        cuda-curand-dev-$CUDA_PKG_VERSION \
        cuda-cusparse-dev-$CUDA_PKG_VERSION \
        cuda-npp-dev-$CUDA_PKG_VERSION \
        cuda-cudart-dev-$CUDA_PKG_VERSION \
        cuda-driver-dev-$CUDA_PKG_VERSION \
        cmake \
        build-essential \
        libboost-all-dev \
        libeigen3-dev \
        libfreeimage-dev \
        libgoogle-glog-dev \
        libgflags-dev \
        libglew-dev \
        freeglut3-dev \
        qt5-default \
        libxmu-dev \
        libxi-dev \ 
        libatlas-base-dev \
        libsuitesparse-dev && \
    cd /tmp && apt-get download gpu-deployment-kit && \
    rm -rf /var/lib/apt/lists/*

RUN mkdir /tmp/gpu-deployment-kit && cd /tmp/gpu-deployment-kit && \
    dpkg -x /tmp/gpu-deployment-kit_*.deb . && \
    mv usr/include/nvidia/gdk/* /usr/local/cuda/include && \
    mv usr/src/gdk/nvml/lib/* /usr/local/cuda/lib64/stubs && \
    rm -rf /tmp/gpu-deployment-kit*

RUN git clone https://ceres-solver.googlesource.com/ceres-solver
    cd ceres-solver
    mkdir build
    cd build
    cmake ..
    make -j
    sudo make install

ENV LIBRARY_PATH /usr/local/cuda/lib64/stubs:${LIBRARY_PATH}
