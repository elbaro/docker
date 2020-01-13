FROM centos:centos8

RUN curl https://sh.rustup.rs -sSf | \
    sh -s -- --default-toolchain nightly -y

ENV PATH=/root/.cargo/bin:$PATH

RUN dnf -y install gcc python36
RUN alternatives --set python /usr/bin/python3
RUN cargo install fd fselect hyperfine ripgrep

