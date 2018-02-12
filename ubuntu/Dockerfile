FROM nvidia/cuda:9.0-cudnn7-devel-ubuntu16.04

RUN apt-get update

RUN apt-get install -y --no-install-recommends \
	software-properties-common apt-transport-https apt-utils \
	build-essential ca-certificates libpng-dev libjpeg-dev libsm-dev

# 3rd party
RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 2930ADAE8CAF5059EE73BB4B58712A2291FA4AD5
RUN echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu xenial/mongodb-org/3.6 multiverse" > /etc/apt/sources.list.d/mongodb-org-3.6.list
RUN add-apt-repository ppa:gophers/archive


RUN apt-get update
RUN apt-get install -y --no-install-recommends \
	git curl wget cmake colordiff htop glances viewnior redis-server p7zip vim \
	zsh zsh-syntax-highlighting libsox-dev ack-grep

# zsh
RUN chmod -R 755 /usr/local/share/zsh/site-functions

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
	cffi tensorboardX matplotlib tqdm h5py backtrace colorama imgaug xgboost librosa pandas pyyaml numpy scipy redis pymongo



# opencv
RUN apt-get install -y libopencv-dev && pip install opencv-python
# mongo db (note: no systemd -> no 'service mongodb start'. need to manually start with `mongod --dbpath .`)
# mongo-c-driver: libssl-dev, libsasl2-dev
RUN apt-get install -y mongodb-org


# pillow, sox
RUN pip install pillow sox
# tensorflow
RUN pip install tensorflow-gpu
# dlib
WORKDIR /tmp
RUN git clone https://github.com/davisking/dlib.git && cd dlib && python setup.py install
# pytorch
WORKDIR /tmp
RUN conda install -c soumith magma-cuda90
RUN pip install http://download.pytorch.org/whl/cu90/torch-0.3.0.post4-cp36-cp36m-linux_x86_64.whl
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



