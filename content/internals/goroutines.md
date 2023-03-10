---
title: Goroutines
type: docs
---

# Goroutines

goroutines start with very small stacks (1024 bytes)
- for this reason gorountine prologues start with checking if we need a bigger stack
- grow stack routine is called `morestack`
- can use `// go:nosplit` pragma to disable this stack checking
- goroutines are cooperatively scheduled

`GOMAXPROCS` controls number of threads to use to distribute goroutines across

`G` struct represents on goroutine
`M` struct represents an os thread

these are defined in runtime/runtime2.go

## goroutine scheduler

## Resources
- [How goroutines work](https://blog.nindalf.com/posts/how-goroutines-work/)
- [internals of goroutines and channels](https://dev.to/girishg4t/internals-of-goroutines-and-channels-397p)
- [scheduling in go](https://www.ardanlabs.com/blog/2018/08/scheduling-in-go-part2.html)
