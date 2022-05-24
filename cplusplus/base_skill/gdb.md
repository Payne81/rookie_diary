# GDB

## Summary

GDB do four main kind of things:

* Start your program, specifying anything that might affect its behavior.
* Make your program stop on specified conditions(`breakpoint`).
* Examine what has happened, when your program has stopped.
* Change things in your program, so you can experiment with correcting the effects of one bug and go on to learn about another. (Change `Routine` dynamically.)

### Invoking GDB

```bash

## launch
gdb program
gdb program core    ## (C++) use -g to gen core file
gdb program 1234    ## specify a process ID as a second argument or use option -p
gdb -p 1234

(gdb) n             ## the command n (next) to advance execution to the next line of the current function
(gdb) s             ## step goes to the next line to be executed in any subroutine
(gdb) bt            ## backtrace
(gdb) l             ## list
(gdb) p             ## print
(gdb) c             ## continue

## set arguments
gdb --args gcc -O2 -c foo.c ## debug gcc, and to set gcc's command-line arguments to '-O2 -c foo.c'
(gdb) run -O2 -c foo.c      ## set arguments in GDB
(gdb) set args -O2 -c foo.c ## set arguments in GDB before `run` ## and `show args`! 

## use shell command
(gdb) shell
(gdb) shell command

## exit: ctrl+d/q
```

## Running Program Under GDB

### Starting a program

Some information should be specified(or use default), This information may be divided into four categories:
(more detail can be find [here](https://sourceware.org/gdb/current/onlinedocs/gdb/Running.html#Running))

* `arguments`
* `environment`, which consists of a set of environment variables and their values.
* `working directory`, use `set cwd`
* `standard input and output`

### Debugging an Already-running Process

```bash
ps -aux | grep program_name     ## get pid
gdb attach process-id           ## if operation not permitted, use sudo
                                ## process-id can be replaced with `pidof program_name`
(gdb) detach                    ## Release the attached process from GDB control
```

### Multithread

GDB provides these facilities for debugging multi-thread programs:

* automatic notification of new threads
* `thread thread-id`, a command to switch among threads
* `info threads`, a command to inquire about existing threads
* *`thread apply [thread-id-list | all] args`, a command to apply a command to a list of threads*
* thread-specific breakpoints
* `set print thread-events`, which controls printing of messages on thread start and exit.
* `set libthread-db-search-path path`, which lets the user specify which libthread_db to use if the default choice isn't compatible with the program.

### Kill & Fork (TODO😁)

### Checkpoint

Checkpoint is a snapshot of a program’s state, which includes changes in memory, registers, and even (within some limits) system state. Effectively, it is like going back in time to the moment when the checkpoint was saved.

To use the checkpoint/restart method of debugging:

```bash
(gdb) checkpoint                        ## Save a snapshot
(gdb) info checkpoints                  ## list the checkpoints
(gdb) restart checkpoint-id             ## Restore the program state that was saved as checkpoint number checkpoint-id.
(gdb) delete checkpoint checkpoint-id   ## Delete the previously-saved checkpoint identified by checkpoint-id.
```

On some systems, address space randomization is performed on new processes for security reasons. Returning to a checkpoint instead of restarting the process makes 
symbols all stay in the same place and avoid the effects of address randomization.

## Stopping and Continuing

### Breakpoint, Watchpoint, Catchpoint

Breakpoint

## Command

Useful commands!

```bash
(gdb) info
```

## References

1. [GDB Documentation](https://sourceware.org/gdb/documentation/)
2. [GDB tutorial](https://www.cnblogs.com/274914765qq/p/6232867.html)

[INDEX](https://payne81.github.io/rookie_diary/)
