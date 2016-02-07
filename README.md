# onion-omega

Docker images for building C and GHC toolchains for the onion omega
IoT device.

First build the image in the `xt` subfolder. It will build the
C toolchain and install it into `/opt/mips-unknown-linux-musl`.
Save that image under the `onion-omega-xt` tag:

    cd xt
    docker build -t onion-omega-xt .
    
Next you can build the GHC cross-compiler from the `ghc`
subdirectory. It will install a GHC cross-compiler into
`/opt/ghc`:

    cd ghc
    docker build -t onion-omega-ghc .
  
If you want to install the toolchains directly on your host,
simply follow the instructions in the Dockerfiles. They are
rather simple and should be easy to follow.
