FROM onion-omega-xt


# gmp is not really needed since we build GHC with integer-simple, but it
# doesn't hurt to have it around.
ADD https://gmplib.org/download/gmp/gmp-6.1.0.tar.xz /opt/source/gmp-6.1.0.tar.xz
RUN tar xf /opt/source/gmp-6.1.0.tar.xz -C /opt/source && \
    cd /opt/source/gmp-6.1.0 && \
    ./configure --host=mips-unknown-linux-musl --prefix=/opt/omega && \
    make install -j4


# ncurses however is required.
ADD https://ftp.gnu.org/pub/gnu/ncurses/ncurses-6.0.tar.gz /opt/source/ncurses-6.0.tar.gz
RUN tar xf /opt/source/ncurses-6.0.tar.gz -C /opt/source && \
    cd /opt/source/ncurses-6.0 && \
    sed -ie '65s/$1/$1 -P/' ncurses/base/MKlib_gen.sh && \
    ./configure --host=mips-unknown-linux-musl --prefix=/opt/omega --enable-overwrite && \
    make install -j4


ADD llvm.list /etc/apt/sources.list.d/llvm.list
RUN apt-get update && apt-get install -y ghc happy alex llvm-3.7
RUN git clone --recursive git://git.haskell.org/ghc.git /opt/source/ghc
ADD build.mk /opt/source/ghc/mk/build.mk
RUN cd /opt/source/ghc && \
    ./boot && \
    ./configure --target=mips-unknown-linux-musl --prefix=/opt/ghc --enable-unregisterised \
        --with-curses-includes=/opt/omega/include --with-curses-libraries=/opt/omega/lib && \
    make install -j4

