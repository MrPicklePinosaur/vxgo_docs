---
title: Elf
type: docs
---

# Go ELF files

Golang produced ELF files have specific quirks that we will discuss.

To be able to identify a go binary even with debug symbols stripped, go includes a note at `.note.go.buildid`. You can look at it with
```
readelf -n <binary>
```

## Resources
- [A deep dive into go binaries](https://qzaidi.github.io/2017/03/05/elf-go-ident/)
- [Notes on the strucure of go ELF files](https://utcc.utoronto.ca/~cks/space/blog/programming/GoBinaryStructureNotes)
- [dissecting go binaries](https://www.grant.pizza/blog/dissecting-go-binaries/) - disassembling go binary using capstone
- [fixing gos linker](https://www.uber.com/en-CA/blog/fixing-gos-linker/)
- [20 part blog series on linker design](https://lwn.net/Articles/276782/)
