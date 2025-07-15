---
tags:
  - 🗎
backlinks:
  - "[[🧰Tools]]"
---
## Statuses

This list is copied from manual, which I believe are most important to understand.

- `D` - uninterruptible sleep (usually IO)
- `I` - Idle kernel thread
- `R` - running or runnable (on run queue)
- `S` - interruptible sleep (waiting for an event to complete)
- `T` - stopped by job control signal
- `t` - stopped by debugger during the tracing
- `X` - dead (should never be seen)
- `Z` - defunct ("zombie") process, terminated but not reaped by its parent
## List all processes

To list all processes, use
`ps -A`

Used mostly when someone wants to determine the PID of the process.
`ps -ef`

I think it is the mostly used combination. It shows the most important info, like PID, status and resources usage.
`ps aux`

the hierarchy of processes
`ps aux --forest`
`pstree` (Cleaner)
`ps aux --forrest` (Requires 'pstree')

## Finding useful information

To be honest... most of people use `grep` with `ps`. But `ps` has enhanced filtering. So why we use `grep`? Because... it is only one command to lear and we already know it! With great filtering comes great number of argument and switches to learn.

Anyway, let's go through some.

`ps -f -u syslog`

shows all processes run by user `syslog`.

`ps -f -C cron`

shows all processes, where the executable is `cron`.

`ps -f -p 1`

shows process with specified PID.

`ps -f --ppid 1`

show all processes, where parent process has PID 1. About parents, children, etc we will talk in future lesson.

With `-p` we can specify more PIDs with coma. Something like `ps -f -p 2543,8843,3456`.

There is much, much more options, views, etc. Here we took a look on the base functionality.

more information is in manual `man ps`