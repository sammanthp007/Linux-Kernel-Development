# Process Management

## Process
A process is a program (object code stored on some media) in the midst of
execution. Processes are, however, more than just the executing program code
(often called the text section in Unix).They also include a set of resources
such as open files and pending signals, internal kernel data, processor state,
a memory address space with one or more memory mappings, one or more threads of
execution, and a data section containing global variables.

## Thread
A process is a program (object code stored on some media) in the midst of
execution. Processes are, however, more than just the executing program code
(often called the text section in Unix).They also include a set of resources
such as open files and pending signals, internal kernel data, processor state,
a memory address space with one or more memory mappings, one or more threads of
execution, and a data section containing global variables.

> Linux has a unique implementation of threads: It does not differentiate
> between threads and processes.To Linux, a thread is just a special kind of
> process.

## Feature
On modern operating systems, processes provide two virtualizations: a
virtualized processor and virtual memory.The virtual processor gives the
process the illusion that it alone monopolizes the system, despite possibly
sharing the processor among hundreds of other processes. Virtual memory lets
the process allocate and manage memory as if it alone owned all the memory in
the system.


