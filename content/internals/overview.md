---
title: "Overview"
type: docs
weight: 100
---

# Golang overview

## Compiler Implementation

Go is just a language specification, thus there are many possible
implementations of the language.
- gc: the standard Go compiler written in go
- emgo: transpiles go to c and then compiles
- tinygo: alternate go compiler with llvm backend (perserves go's memory model, this implies garbage collection)
- gccgo: alternate go compiler implementation with more optimizations (supports same platforms as gcc), sometimes has bad performance (due to poor escape analysis), also uses dynamic linking

We will be porting gc, as it is the most supported and modern. Since one
objective is to be able to run existing software on VxWorks, we want to choose
a version that most likely supports the software we wish to run.

## Other Tools/Terminology

GC: is go's garbage collector (GC), is a non-moving mark and sweep garbage collector
cgo: lets go call c code from go
TLS: thread local storage
