FROM ubuntu@16.04

RUN apt-get update
RUN apt-get install -y gawk bison flex gperf cvs texinfo automake \
    libtool ncurses-dev g++ subversion python-dev libexpat1-dev cmake \
    git wget build-essential help2man libtool libtool-bin

RUN git clone https://github.com/crosstool-ng/crosstool-ng.git /opt/source/xt
RUN cd /opt/source/xt && \
    ./bootstrap && \
    ./configure --prefix=/usr && \
    make && \
    make install

RUN mkdir /var/run/xt
ADD defconfig /var/run/xt/defconfig
RUN cd /var/run/xt && \
    ct-ng defconfig && \
    ct-ng source && \
    ct-ng build.$(grep -c ^processor /proc/cpuinfo) && \
    rm -rf /var/cache/xt

ENV TARGET=mips-unknown-linux-musl
ENV PATH=/opt/xt/$TARGET/bin:$PATH
