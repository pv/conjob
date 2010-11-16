======
Conjob
======

Do you need to run a huge number of batch jobs on a single machine?
Are you frustrated with manually launching processes in a screen(1)?
Are cluster computing software such as SLURM and QSUB overkill for you?

If yes, then Conjob may be what you are looking for:

- Run batch jobs in the background on a single machine.
- Capture and log output.
- Limit number of running processes by machine load and available memory.
- Submit jobs in batches.
- Job priorities, process control, suspension, etc.

Synopsis
--------

::

  conjob [options] COMMAND [...]

  Process job controller, letting a limited number of jobs run at the same
  time.

  Commands:
    list                List scheduled PIDs
    schedule [COUNT]    Perfom scheduling, starting/stopping processes
    setprio JIDS PRIO   Set a priority for a PID
    run CMD             Run a command and put the process in the queue
    bg CMD              Run a command in the background and insert to queue
                        Redirect the output to a file in ~/.conjob.log/
    bg_many < CMDS      Queue many commands at once; one per line
    kill JIDS           Kill jobs
    tail JIDS           Tail -f logfiles
    less JIDS           Page through logfiles
    cleanup JIDS        Remove completed jobs from the job list
    requeue JIDS        Kill and re-queue given jobs
    dump_jobs [FILE]    Dump a job listing to FILE or stdout
    load_jobs [FILE]    Load a job listing from FILE or stdin

    'JIDS' can be a comma separated list of JIDs, or a shell glob pattern.
    The syntax '{MIN-MAX}' matches all integers from MIN to MAX.
    Prepending '/' to the pattern makes it match also completed jobs,
    '@' the command lines, '%' the PIDs.

Configuration
-------------

Configuration goes into ``~/.conjob``::

  # Max number of simultaneous processes
  nprocs = 8
  # Max load average
  loadavg = 8.0
  # Nice of processes
  nice = 20
  # Maximum amount of memory to hog
  max_mem_percentage = 75
  # Minimum free virtual memory (avoid swapping)
  min_vm_free = 3e9
  # Pager
  pager = less -S +k

