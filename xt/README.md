Image with cross-compiler tools which target the Onion Omega device.
The tools are installed into `/opt/xt/mips-unknown-linux-musl`.

The Onion Omega image is based on OpenWRT which uses an old version
of uClibc. That version of uClibc is not standards-conformant, and GHC
unfortunately can't be compiled against that. So I chose musl as the
libc. That means you have to statically compile any applications you
want to build with this toolchain (`gcc -static` or
`ghc -static -optl-static`).

If you have an autotools project you can set the host on the commandline
when invoking the `./configure` script:

```
export PATH=/opt/xt/mips-unknown-linux-musl/bin:$PATH
./configure --host=mips-unknown-linux-musl
```
