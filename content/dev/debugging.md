---
title: "Debugging"
type: docs
---

# Debugging the Go toolchain

# Debugging the go compiler

The `-toolexec` flag lets you specify a command to run each go tool with. This opens up the possibility of debugging go subcommands.

One issue is that in builds, go also captures tool output to extract the buildid.


## Debugging Go Tools

Go invokes a variety of tools during the build process, notable `link`. If we wish to debug the linker, we can't simply attach a debugger to `go build`, since go build will spawn `go tool link`. Thus, we need to use `-toolexec` to invoke a wrapper script that will call the debugger on whatever tool we wish to run.

Another slight caveat is that go will read the standard output of the tool it calls to grab the buildid, so we actually need to invoke the debugger on headless mode and connect to it to be able to debug it properly.

TODO: investigate src/cmd/go/internal/trace/
TOOD: investigate TOOLSTASH

## Delve

## GDB

## Coredumps

Use `GOTRACEBACK=crash` to get coredumps on crashes

# Resources
- [Reproducing go binaries](https://words.filippo.io/reproducing-go-binaries-byte-by-byte/)
- [Go debugging with delve coredumps](https://medium.com/a-journey-with-go/go-debugging-with-delve-core-dumps-384145b2e8d9)
