NOTE: While this encryption program works, testing shows it is not as
fast or as secure as my original MrrCrypt project. So as of now, have no
plans to continue developing this. If you are interested in an encryption
algorithm based on mirror fields, please see the original [blckroot](https://github.com/blck-root/blckroot64).
If for some reason you are still interested in this project, keep reading.

BlckRoot64
==========

The original purpose of this project was to implement a mirror field
encryption algorithm that only supports 64 characters (the original supports
256). The idea was to encode all non-encrypted input as base64 prior to
processing it through the encryption algorithm, thus only requiring
support for 64 characters.

In theory, this should have given me speed gains over the original version
that supports 256 characters, due to a smaller mirror field size and a
speedier traversal process. Unfortunately I quickly found that I would have
to sacrifice an inherent trait to mirror field encryption that makes it
unique... I would have to create a command-line option to specify whether
we are encrypting or decrypting, which would then allow me to know what
base64 operations were required for the input and output. I did not want
to make this sacrifice.

I continued to play around with various other possibilities to reduce the
size of the mirror field, and I eventually settled on a solution that only
supports 16 characters, with a mirror field size of 4x4. The idea was to
split each byte into two 4-bit values, each with only 16 possible characters,
and feed them through the mirror field. In order to increase both randomness
and key size (a 4x4 mirror field can be brute-forced pretty quickly) I
implemented support for an array of mirror fields such that the algorithm
utilizes the mirror fields in the array in a round-robin fashion for each
character it processes.

This program works, but as it stands, it does not perform better than my
original MrrCrypt project. It is slower and it fails many industry-standard
tests for randomness. For this reason I do not suggest using it.

Download and Install
--------------------

Download and Build:

```
$ git clone https://github.com/blck-root/blckroot64.git
$ cd blckroot64
$ make
```

Install:

```
$ make install
```

Uninstall:

```
$ make uninstall
```

Further Documentation
-----------------------

I do not intend to provide documentation for this project beyond what you
already see in this document. However the usage is identical to the original
[blckroot](https://github.com/blck-root/blckroot), so you can
see the documentation for that project for more info.
