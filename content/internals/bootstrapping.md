---
title: Bootstrapping
type: docs
---

# Bootstrapping

Many things occur before the main function of a golang executable even gets called. We will cover all the set up and bootstrapping golang performs here.


entry point call stack (for executables) looks like
`_rt0_vxworks_amd64` -> `_rt0_amd64` -> `rt0_go`


rt0_go then calls:
- runtime.args
- runtime.osinit
- runtime.schedinit
- runtime.newproc
- runtime.mstart -> mstart0 (runtime/proc.go) -> mstart1

mstart1 then reads the `m` variable (current goroutine) and executes the startfn (main)
