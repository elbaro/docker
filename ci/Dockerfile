FROM archlinux:latest

RUN pacman -Syyu --noconfirm --noprogressbar \
	git clang python python-pip go rustup wget p7zip
RUN rustup install nightly && rustup default nightly
RUN pip install cpplint
RUN cargo install fd fselect hyperfine ripgrep

# locale
ENV LANG=en_US.UTF-8
RUN echo "en_US.UTF-8 UTF-8" >> /etc/locale.gen && locale-gen
