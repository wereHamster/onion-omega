FROM ubuntu@16.04

RUN apt-get update
RUN apt-get install -y gawk bison flex gperf cvs texinfo automake \
    libtool ncurses-dev g++ subversion python-dev libexpat1-dev cmake \
    git wget build-essential help2man libtool libtool-bin

RUN git clone https://github.com/crosstool-ng/crosstool-ng.git /opt/source/xt
RUN cd /opt/source/xt && ./bootstrap && ./configure --prefix=/usr && make && make install

RUN useradd -m xt
RUN mkdir -p /var/cache/xt /opt/xt && chown xt /var/cache/xt /opt/xt

ADD defconfig /home/xt/defconfig
RUN su -lc 'ct-ng defconfig && ct-ng source && ct-ng build.$(grep -c ^processor /proc/cpuinfo)' xt

ENV TARGET=mips-unknown-linux-musl
ENV PATH=/opt/xt/$TARGET/bin:$PATH
