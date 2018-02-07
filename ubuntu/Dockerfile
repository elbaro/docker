FROM nvidia/cuda:9.0-cudnn7-devel-ubuntu16.04

RUN apt-get update
RUN apt-get install -y --no-install-recommends software-properties-common
RUN add-apt-repository ppa:gophers/archive
RUN apt-get update
RUN apt-get install -y --no-install-recommends \
	git curl wget cmake colordiff htop glances viewnior redis-server p7zip vim \
	zsh zsh-syntax-highlighting libsox-dev

# slimzsh
RUN git clone --recursive https://github.com/changs/slimzsh.git ~/.slimzsh

# go 1.9
RUN apt-get install -y --no-install-recommends golang-1.9-go

# miniconda
WORKDIR /tmp
RUN curl -LO https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh
RUN bash Miniconda3-latest-Linux-x86_64.sh -p /miniconda -b
RUN rm Miniconda3-latest-Linux-x86_64.sh
ENV PATH=/miniconda/bin:${PATH}
RUN conda update -y conda


RUN pip install \
	cffi tensorboardX matplotlib tqdm h5py backtrace colorama imgaug xgboost librosa pandas pyyaml numpy scipy

# pillow, sox
RUN pip install pillow sox
# tensorflow
RUN pip install tensorflow-gpu
# dlib
WORKDIR /tmp
RUN git clone https://github.com/davisking/dlib.git && cd dlib && python setup.py install
# pytorch
WORKDIR /tmp
RUN git clone --recursive https://github.com/pytorch/pytorch.git && cd pytorch && python setup.py install
# torchaudio
WORKDIR /tmp
RUN git clone https://github.com/pytorch/audio.git && cd audio && python setup.py install
# torchvision
WORKDIR /tmp
RUN git clone https://github.com/pytorch/vision.git && cd vision && python setup.py install
# tinder
WORKDIR /tmp
RUN git clone https://github.com/elbaro/tinder.git && cd tinder && python setup.py install
# rustup -> rust
RUN curl https://sh.rustup.rs -ssf | sh -s -- -y --default-toolchain nightly

# zshrc
RUN curl -o ~/.zshrc https://raw.githubusercontent.com/elbaro/dotfiles/master/zshrc

WORKDIR /data

# Expose 10 ports
EXPOSE 10000-10010

# locale
RUN apt-get install -y locales
RUN locale-gen en_US.UTF-8
ENV TZ=Asia/Seoul

ENTRYPOINT ["/bin/sleep", "infinity"]

