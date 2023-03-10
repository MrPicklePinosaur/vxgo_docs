---
title: "Compiling Go"
type: docs
---

# Compiling Go

## Build system

The go compiler can be built by running `src/make.bash`. Once built, quicker
builds can be done with
```sh
$GOROOT/bin/go install cmd/compile
```
You can also build any other tools (such as `link`), similarly:
```sh
$GOROOT/bin/go install cmd/link
```

Built go binaries are located in `bin`. Go also makes calls to subcommands
(such as `compile` and `link`), where are located in `pkg/tool/<arch>/`

The other tools are built with a go script `src/cmd/dist/build.go`.

## Environment variables

- GOARCH: the architecture we are compiling for
- GOOS: the operating system we are compiling for
- CGO_ENABLED: enable cgo
- GOROOT: where to install built compiler
- GCFLAGS: flags to pass to the go compiler

These are used by the `make.bash` script
- GOROOT_BOOTSTRAP: which bootstrapping compiler to use
