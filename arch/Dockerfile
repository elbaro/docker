FROM greyltc/archlinux-aur

RUN pacman -S --noconfirm \
	git \
	pacutils \
	perl-libwww \
	perl-term-ui \
	perl-json \
	perl-data-dump \
	perl-lwp-protocol-https \
	perl-term-readline-gnu


RUN pacman -S --noconfirm \
	git python python-pip colordiff go rustup htop glances viewnior redis wget p7zip vim \
	zsh zsh-syntax-highlighting zsh-completions \
	python-tensorflow-opt-cuda \
	python-pytorch-cuda \
	sox

RUN su docker -c 'pacaur -S --noprogressbar --noedit --noconfirm zsh-autosuggestions command-not-found dlib python-pillow-simd'

RUN git clone --recursive https://github.com/changs/slimzsh.git ~/.slimzsh

RUN pip install \
	cffi tensorboardX matplotlib tqdm h5py backtrace colorama imgaug xgboost librosa pandas


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
RUN rustup install nightly && rustup default nightly
# zshrc
RUN curl -o ~/.zshrc https://raw.githubusercontent.com/elbaro/dotfiles/master/zshrc

WORKDIR /data

# Expose 10 ports
EXPOSE 10000-10010

# locale
ENV LANG=en_US.UTF-8
ENV TZ=Asia/Seoul
RUN echo "en_US.UTF-8 UTF-8" >> /etc/locale.gen && locale-gen

ENTRYPOINT ["/bin/sleep", "infinity"]

