Image with cross-compiler tools which target the Onion Omega device.
The tools are installed into `/opt/xt/mips-linux-musl`.

The Onion Omega image is based on OpenWRT which uses an old version
of uClibc. That version of uClibc is not standards-conformant, and GHC
unfortunately can't be compiled against that. So I chose musl as the
libc. That means you have to statically compile any applications you
want to build with this toolchain (`gcc -static` or
`ghc -static -optl-static`).

The CPU is a MIPS32 24Kc, implements up to the mips32r2 ISA. The board
has no FPU so all software must be compiled with softfloat. ABI is set
to o32.

If you have an autotools project you can set the host on the commandline
when invoking the `./configure` script:

```
export PATH=/opt/xt/mips-linux-musl/bin:$PATH
./configure --host=mips-linux-musl
```
