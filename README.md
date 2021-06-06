# Our style/testing guidelines for writing quality C code which meets our standards for portability and robustness

These are not strict but rather suggestions for how to write code that "fits in" with the rest of our projects.

1) avoid use of // comments
2) use a c89 compatible subset of C wherever possible
3) Avoid using compiler-specific extensions such as Goto labels even when there would be a tangible performance gain, or provide a non-compiler-specific alternative based on compile DEFINEs (`#ifdef __GNUC__`)
4) run lints over your code, compile with -pedantic,
5) Pay attention to the [C89](http://port70.net/~nsz/c/c89/c89-draft.html) and [C99](http://port70.net/~nsz/c/c99/n1256.html) standards.
6) Read the Suckless coding guidelines, we do not strictly follow them but we like them: http://suckless.org/coding_style/
7) Compile and test your code on other architectures, at the very least on i386 if you're on x86_64! You get it for basically free.
8) Your makefile should always include a `clean` target with standard and expected behavior. if you are writing a utility, you should implement `install uninstall` with expected behavior. The default action when invoking `make` (I.E. the first defined target) should always be the default and expected build of your 
9) avoid using C++ Keywords such as `this`
10) Use `CFLAGS CC OPTLEVEL` and other makefile variables so that configuration compilation is easier. CC should either be `gcc`, `cc` or `tcc` by default, it should never be any others.
11) If a compiler extension is used or highly non-portable code must be used in a project, implement checks at compiletime for the correct environment. Use #error to emit compiletime errors for incompatible environments. Attempt to provide alternatives.
12) if you want to prevent your code from compiling on a specific compiler as a form of protest (E.g. preventing people from compiling your code with MSVC) use compiletime checks against compiler defines. 
13) be extremely weary of malloc alignment. Many implementations are non-conformant and will not, for instance, allocate memory aligned properly for SSE vectorized ops. Assume that malloc aligns to sizeof(double).
