FROM onion-omega-xt


# gmp is not really needed since we build GHC with integer-simple, but it
# doesn't hurt to have it around.
ADD https://gmplib.org/download/gmp/gmp-6.1.0.tar.xz gmp-6.1.0.tar.xz
RUN tar xf gmp-6.1.0.tar.xz && \
    cd gmp-6.1.0 && \
    ./configure --host=mips-unknown-linux-musl --prefix=/opt/omega && \
    make install -j4


# ncurses however is required.
ADD https://ftp.gnu.org/pub/gnu/ncurses/ncurses-6.0.tar.gz ncurses-6.0.tar.gz
RUN tar xf ncurses-6.0.tar.gz && \
    cd ncurses-6.0 && \
    sed -ie '65s/$1/$1 -P/' ncurses/base/MKlib_gen.sh && \
    ./configure --host=mips-unknown-linux-musl --prefix=/opt/omega --enable-overwrite && \
    make install -j4


RUN git clone --recursive git://git.haskell.org/ghc.git
ADD build.mk ghc/mk/build.mk
RUN cd ghc && \
    ./boot && \
    ./configure --target=mips-unknown-linux-musl --prefix=/opt/ghc --enable-unregisterised && \
    make install -j4

