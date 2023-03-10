---
title: "Debugging"
type: docs
---

# vxworks specific debugging info

## debugging backends

exposing port vs qemu gdb backend

tTcf are for communicating with eclipse
- generic debugger framework
- this is the older solution for debugging 
- in modern versions we can build vxworks with gdbserver support

TCF_GDB_RSP for vsb config option to include gdbserver
include DEBUG_AGENT in VIP
also include STANDALONE_SYMBOL_TABLE in vxworks image

wrdbg is a gdb-like shell (it translates commands to TCF commands), its not real gdb

debug symbols are used for assigning names to memory
sources are used for associating source code lines to current position

https://docs.windriver.com/bundle/vxworks_remote_debugging_with_gdbserver_tutorial_22_09/page/tjn1612816505665.html

# Debugging usin wrdbg

We can use `wrdbg` thats bundled with the sdk to debug vxworks.

Start one vxwork simulator with our `vxworks_boot` script, and on another terminal, start up `wrdbg` and run.

```
target connect vxworks7:localhost:1534 -kernel ./vxsdk/bsps/itl_generic_3_0_0_2/vxWorks -logdir /tmp
```

You can list the current processes with
```
ps
```

and attach to a spawn process with
```
attach <process>
```

One fun aspect is that `wrdbg` does not support DWARFV4 debugging symbols that the go compiler generates.

# Debugging with vxgdb

A better option is to use gdbserver and `vxgdb`, which is real gdb. You need to build a version of the SDK with gdbserver support first. See [docs](https://docs.windriver.com/bundle/vxworks_remote_debugging_with_gdbserver_tutorial_22_09/page/tjn1612816505665.html)

Once vxworks qemu is running, you can start up `vxgdb` and run
```
(gdb) target extended-remote tcp:127.0.0.1:2345
```

From here, copy the executable you wish to debug with
```
(gdb) remote put <binary> /ram0/<binary>
(gdb) set remote exec-file /ram0/<binar>
```

And to debug, just run
```
(gdb) start
```

Also need a copy of `libc.so.1` and `libllvm.so.1`. Copy it to your working diretory from the sdk path `vxsdk/sysroot/usr/lib/common`

- [docs](https://docs.windriver.com/bundle/vxworks_remote_debugging_with_gdbserver_tutorial_22_09/page/nsh1612989711588.html)

## spawning RTPs from VxWorks command shell

To immediately suspend program after launching
```
rtp exec -s <executable>
```

## Core dumps

core dump support needs to be first included in your VIP, you can enable it under build configuration and including `FOLDER_CORE_DUMP_RTP`

- [Configuring RTP core dumps](https://academy.windriver.com/vxworks-core-dumps/1373863/scorm/1drubvxklea90)
- [Windriver Debug Shell](https://labs.windriver.com/downloads/toolkit/wrdbg_tools/lib/python/doc/html/wrdbg/gettingstarted.html): not sure if outdated, may only work with RTP
