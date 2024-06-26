## Killing Processes

### Process Control Using Signals

Signals are software interrupts delivered to processes, indicating events such as errors, I/O requests, or explicit commands. Here are key signals used for process management:

| Signal Number | Short Name | Purpose |
|---------------|------------|---------|
| 1             | HUP        | Hangup, termination of controlling process, or reload configuration. |
| 2             | INT        | Interrupt, terminates program (Ctrl+c). |
| 3             | QUIT       | Quit, similar to INT but adds core dump at termination (Ctrl+\). |
| 9             | KILL       | Unblockable, abrupt termination (always fatal). |
| 15            | TERM       | Terminate, polite request for program termination (can be handled). |
| 18            | CONT       | Continue, resume a stopped process. |
| 19            | STOP       | Unblockable, suspend a process. |
| 20            | TSTP       | Stop, suspend a process (Ctrl+z, unlike STOP can be handled). |

### Sending Signals

- **kill**: Sends a signal to a process by PID. Despite its name, `kill` can send any signal.
  ```bash
  $ kill -9 5194
  ```

- **killall**: Sends a signal to all processes matching a command name.
  ```bash
  $ killall control
  ```

- **pkill**: Sends a signal based on process attributes (name, user, etc.).
  ```bash
  $ pkill -U user
  ```

### Logging Users Out

To administratively log out users, identify sessions using `w`, then terminate processes accordingly:

- Identify sessions:
  ```bash
  $ w
  ```
  
- Terminate processes by TTY or user:
  ```bash
  $ pkill -t tty3
  $ pkill -u bob
  ```

- Use `pstree` to view process relationships and terminate them:
  ```bash
  $ pstree -p bob
  $ pkill -P 8391
  ```

### Recommendations

- **Signal Sequence**: Prefer `SIGTERM` (15) for graceful termination, followed by `SIGINT` (2), and then `SIGKILL` (9) if necessary.
  
- **Root Privileges**: Required to terminate processes owned by other users.

### References

- GNU C Library Reference Manual:
  - [Signal Handling](https://www.gnu.org/software/libc/manual/html_node/Signal-Handling.html)
  - [Processes](https://www.gnu.org/software/libc/manual/html_node/Processes.html)
  
- Man Pages: `kill(1)`, `killall(1)`, `pgrep(1)`, `pkill(1)`, `pstree(1)`, `signal(7)`, `w(1)`
