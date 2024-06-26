## Controlling Jobs

### Jobs and Sessions Overview

Job control in Bash allows for managing multiple processes within a single terminal session. Here are key concepts:

- **Job**: Associated with each command or pipeline executed from the shell prompt. All processes in a pipeline belong to the same job and process group.
  
- **Foreground Process**: A job that can read input and receive signals from the terminal where it was initiated. Only one job can be in the foreground at a time.
  
- **Background Process**: A job that runs independently of the foreground, initiated by appending `&` to the command line. It cannot read input from the terminal but can write to it.

- **Session**: Each terminal operates within its own session, comprising a foreground process and multiple background processes. A job belongs to the session of its controlling terminal.

### Running Jobs in the Background

To start a job in the background:
```bash
$ sleep 10000 &
[1] 5947
```
- `sleep 10000 &`: Initiates the `sleep` command in the background, showing job number `[1]` and its PID `5947`.

To list all jobs tracked by Bash:
```bash
$ jobs
[1]+ Running sleep 10000 &
```

### Bringing Jobs to Foreground and Background

- **Foreground**: Use `fg` with the job ID (`%1` in this case) to bring a background job to the foreground:
  ```bash
  $ fg %1
  sleep 10000
  ```

- **Background**: Press `Ctrl+z` to suspend a foreground process and then use `bg` with the job ID to resume it in the background:
  ```bash
  $ ^Z
  [1]+ Stopped sleep 10000
  $ bg %1
  [1]+ sleep 10000 &
  ```

### Managing Jobs

- **Listing Job Information**: Use `ps j` to display detailed information about jobs, including PID, PPID, PGID, SID, and state:
  ```bash
  $ ps j
   PPID   PID  PGID   SID TTY      TPGID STAT   UID   TIME COMMAND
   2768  5947  5947  2768 pts/0    6377  S      1000  0:00 sleep 10000
  ```

- **Exiting Sessions**: If there are suspended jobs, attempting to exit a terminal session will prompt a warning. To force exit with suspended jobs, use `exit` again immediately.

### References

- Bash info page (The GNU Bash Reference Manual): [Bash Manual](https://www.gnu.org/software/bash/manual)
- `bash(1)`, `builtins(1)`, `ps(1)`, `sleep(1)` man pages
