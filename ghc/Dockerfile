FROM onion-omega-xt


# ncurses however is required.
ADD https://ftp.gnu.org/pub/gnu/ncurses/ncurses-6.0.tar.gz /opt/source/ncurses-6.0.tar.gz
RUN tar xf /opt/source/ncurses-6.0.tar.gz -C /opt/source && \
    cd /opt/source/ncurses-6.0 && \
    sed -ie '65s/$1/$1 -P/' ncurses/base/MKlib_gen.sh && \
    ./configure --host=mips-unknown-linux-musl --prefix=/opt/omega --enable-overwrite && \
    make install -j$(grep -c ^processor /proc/cpuinfo)


ADD llvm.list /etc/apt/sources.list.d/llvm.list
RUN apt-get update && apt-get install -y ghc happy alex llvm-3.7
RUN git clone --recursive git://git.haskell.org/ghc.git /opt/source/ghc
ADD build.mk /opt/source/ghc/mk/build.mk
ADD ghc.patch /opt/source/ghc/ghc.patch
RUN cd /opt/source/ghc && \
    git apply ./ghc.patch && \
    ./boot && \
    ./configure --target=mips-unknown-linux-musl --prefix=/opt/ghc --enable-unregisterised \
        --with-curses-includes=/opt/omega/include --with-curses-libraries=/opt/omega/lib && \
    make -j$(grep -c ^processor /proc/cpuinfo) && make install

