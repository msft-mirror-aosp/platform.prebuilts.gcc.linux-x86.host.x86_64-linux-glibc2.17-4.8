# Host glibc sysroot

Here lie the bones of a prebuilt glibc 2.17, the current host Linux sysroot.

Full version updates have historically been painful. They also annoy users.
This is the sysroot used to build the NDK and other host tools shared with
app developers, not just OS developers, and even OS developers outside Google
often seem to prefer (or at least "are required by corporate policy") to
stick to older host OS versions with old glibc versions.

We do not currently plan to update to a newer glibc. Our hope is to be able to
move to musl instead, which will also offer the option of shipping static host
executables.

In the meantime, we have been taking targeted updates to these headers.

In particular, adding missing constants is almost always fine, whereas
adding missing function declarations doesn't help anyone (though we could
potentially add a static inline, but that's not something we've done yet).

In the ideal case, you can simply copy the current glibc header over the old
one and it "just works". In such cases, just remember to include the glibc
version number that you're updating to in the commit message.

Other cases can be a lot harder. Sometimes there are changes you don't want or
can't take in the same file, for example. Or there might have been a
sufficiently large refactoring of transitive includes that you end up touching
tens of headers when all you really wanted to do was add one missing constant.
These kinds of cases are probably worth discussing with the OWNERS before you
get too deep in the weeds!