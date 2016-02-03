Image with cross-compiler tools which target the Onion Omega device.
The tools are installed into `/opt/xt/mips-unknown-linux-musl`.

If you have an autotools project you can set the host on the commandline
when invoking the `./configure` script:

```
export PATH=/opt/xt/mips-unknown-linux-musl/bin:$PATH
./configure --host=mips-unknown-linux-musl
```
