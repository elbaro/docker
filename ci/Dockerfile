FROM archlinux

RUN pacman -Sy --noconfirm --noprogressbar reflector
RUN reflector --verbose --age 12 --protocol https --sort rate --save /etc/pacman.d/mirrorlist
RUN pacman -Syyu --noconfirm --noprogressbar \
	git clang python python-pip flake8 go rustup wget p7zip
RUN rustup install nightly && rustup default nightly
RUN pip install cpplint flake8
RUN cargo install fd fselect hyperfine ripgrep

# locale
ENV LANG=en_US.UTF-8
RUN echo "en_US.UTF-8 UTF-8" >> /etc/locale.gen && locale-gen

