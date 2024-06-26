## Monitoring Processes

### Describing Load Average

Load average in Linux reflects the system's workload over time, encompassing processes ready to execute or waiting for I/O completion. It's calculated every five seconds as an exponential moving average over 1, 5, and 15-minute periods. This metric aids in gauging system resource demand and performance.

### Understanding Load Average Calculation

- **Components**: Includes processes ready to run (`R`) or waiting for I/O (`D`).
- **Indicators**: Reflects CPU and I/O demands; high load despite low CPU usage suggests I/O bottlenecks.
- **Interpretation**: Three load average values (1-minute, 5-minute, 15-minute) indicate current system load trends.

### Interpreting Displayed Load Average Values

Using `uptime`, load averages are displayed as:
```bash
$ uptime
 15:29:03 up 14 min, 2 users, load average: 2.92, 4.48, 5.20
```
Values represent load over 1, 5, and 15-minute intervals. Dividing by the number of CPUs helps gauge per-CPU load:
```plaintext
load average: 2.92, 4.48, 5.20
divide by number of logical CPUs (e.g., 4)
per-CPU load average: 0.73, 1.12, 1.30
```
- Values <1 indicate optimal resource use; >1 suggests potential saturation.

### Real-time Process Monitoring with `top`

- **Overview**: Provides dynamic process information, refreshable at intervals, with sortable columns:
  - `PID`: Process ID
  - `USER`: Process owner
  - `VIRT`: Virtual memory usage
  - `RES`: Resident memory usage
  - `S`: Process state (`R`, `D`, `S`, `T`, `Z`)
  - `TIME`: CPU time
  - `COMMAND`: Process name

### Fundamental Keystrokes in `top`

- **Navigation**: Use interactive keystrokes:
  - `?` or `h`: Help
  - `l`, `t`, `m`: Toggle load, threads, memory views
  - `s`: Adjust refresh rate
  - `k`: Kill a process by PID
  - `r`: Renice a process by PID
  - `u`, `Shift+u`: Filter processes by user
  - `Shift+m`, `Shift+p`: Sort processes by memory or CPU usage
  - `q`: Quit `top`

### References

- Man Pages: `ps(1)`, `top(1)`, `uptime(1)`, `w(1)`

For detailed exploration and management of Linux processes, understanding load average and utilizing tools like `top` are essential for efficient system administration.
