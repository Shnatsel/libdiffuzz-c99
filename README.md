## C99 implementation of libdiffuzz, the poor man's Memory Sanitizer

[Libdiffuzz](https://github.com/Shnatsel/libdiffuzz) a drop-in replacement for OS memory allocator that can be used to detect uses of uninitialized memory. It is designed to be used in case [Memory Sanitizer](https://clang.llvm.org/docs/MemorySanitizer.html) is not available for some reason. See [libdiffuzz README](https://github.com/Shnatsel/libdiffuzz) for information on usage and how it works.

This is a portable C99 implementation that can be used on really obscure CPUs or operating systems where Rust compiler is not available (e.g. OpenRISC or Haiku). It is portable in the sense that the code is so trivial and dependency-free that you can easily port it, not in the sense that it will work as-is anywhere, which is notoriously hard to do in C.

Note in this implementation the counter access is not atomic, so uninitialized reads in multi-threaded programs may not be reliably detected.

## Why rewrite in Rust?

In a word, **portability.**

Making the C implementation thread-safe and portable in the "you can run this unaltered code anywhere" sense would require a complex build system, and C build systems are a circle of hell. I did not want to find myself continuously patching `.in.in` files or yet another DSL for years.

By contrast, in Rust I can write a program once and expect it to work everywhere with a Rust compiler, even one as low-level as a memory allocator.

## See also

[libdislocator](https://github.com/mirrorer/afl/tree/master/libdislocator), poor man's [Address Sanitizer](https://clang.llvm.org/docs/AddressSanitizer.html) that also works with black-box binaries. libdiffuzz-c99 is based on libdislocator code.
