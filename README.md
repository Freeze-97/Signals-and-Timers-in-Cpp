# 🚦⏱️ Signals and Timers in C++

## Overview
This lab is designed to deepen understanding of **signals** and **timers** in C++. It demonstrates how these mechanisms interact with processes, and how we can use them to monitor execution time across different categories: real time, virtual time, and prof time.

### 🎯 Objectives
- Understand and use UNIX signals and how they affect program behavior.
- Use interval timers (`ITIMER_REAL`, `ITIMER_VIRTUAL`, and `ITIMER_PROF`) to track time.
- Compare CPU and IO-bound workloads using signal-based timing.

## 🗒️ Description
In this lab, a program is created that executes one of three task types:
- **CPU-intensive**
- **IO-intensive**
- **Mixed CPU and IO**

Using `setitimer()` and signal handling, the program tracks how much time has elapsed from three perspectives:
- **Real time** – Wall-clock time (triggered by `SIGALRM`)
- **Virtual time** – Time spent executing the program in user space (`SIGVTALRM`)
- **Prof time** – Combined time in user and kernel space (`SIGPROF`)

Signals are handled centrally and are used to print statistics, stop tasks, and update timing counters.

## ⚙️ How It Works
- The user runs the program with one argument: `cpu`, `io`, or `cpu-io`.
- Based on the input, a corresponding task is run (`TestTask` interface and its subclasses).
- Multiple timers are started using `setitimer()`.
- When a timer interval expires, it triggers a signal that is handled by `signalHandler()`.
- When interrupted (e.g., with `SIGUSR2` or `SIGTERM`), the program gracefully stops and prints the final timing results.

## 🧑‍🔧 Usage

### 🛠️ Compile
Run the following command to compile everything:

```bash
make
```

### ▶️ Run
To execute the program:
```bash
./Lab3 <mode>
```

Where <mode> is one of:
- ***cpu*** – for CPU-intensive task
- ***io*** – for IO-intensive task
- ***cpu-io*** – for combined task

### 📡 Signals
You can interact with the running program using signals:
- ***SIGUSR1***: Print current timer values
- ***SIGUSR2*** or ***SIGTERM***: Gracefully stop the program and show final stats
- ***CTRL+C*** (***SIGINT***): Immediate interruption
