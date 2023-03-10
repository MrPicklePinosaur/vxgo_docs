---
title: Assembly
type: docs
---

# Golang Assembly

pseudo registers
- PC: program counter
- SB: static base, refers to the start of address space of program
- SP: stack pointer
- FP: (virtual) frame pointer, used to reference arguments
    - 0(FP) is first arg, 8(FP) is second arg etc

user defined symbols are written relative to FP (args and locals) or SB (for globals)

values prefixed with dollar sign, (ex $1, $16) are constant values


function declaration

notes
- functions always end with some type of jump (no fallthrough allowed)
- FUNCDATA and PCDATA are for garbage collector use
- golang mov (and a lot of other instructions) have inversed arguments, MOV A B means mean A to B

<!-- compiler flags -->
<!-- - `-fpie`: position indepdendent code (to support ASLR) -->
<!-- - `` -->

## Resources
- [gointernals book golang assembly](https://github.com/teh-cmc/go-internals/blob/master/chapter1_assembly_primer/README.md#pseudo-assembly)
- [(official) a quick guide to go's assembler](https://go.dev/doc/asm)
- [go asm lang reference](https://quasilyte.dev/blog/post/go-asm-complementary-reference/)
- [calling go functions from asm](https://quasilyte.dev/blog/post/call-go-from-jit/)
