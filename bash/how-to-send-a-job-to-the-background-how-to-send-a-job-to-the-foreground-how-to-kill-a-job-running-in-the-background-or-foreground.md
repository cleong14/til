# 2024-03-19 - TIL - How to Send a Job to the Background? How to Send a Job to the Foreground? How to Kill a Job Running in the Background or Foreground?

How to send a job to the background, how to send a job to the foreground, and how to kill a job running in the background or foreground?


## Usage

```sh
jobs

Display status of jobs in the current session.
More information: <https://manned.org/jobs>.

- Show status of all jobs:
    jobs

- Show status of a particular job:
    jobs %job_id

- Show status and process IDs of all jobs:
    jobs -l

- Show process IDs of all jobs:
    jobs -p


bg

Resume suspended jobs (e.g. using `Ctrl + Z`), and keeps them running in the background.
More information: <https://manned.org/bg>.

- Resume the most recently suspended job and run it in the background:
    bg

- Resume a specific job (use `jobs -l` to get its ID) and run it in the background:
    bg %job_id


fg

Run jobs in foreground.
More information: <https://manned.org/fg>.

- Bring most recently suspended or running background job to foreground:
    fg

- Bring a specific job to foreground:
    fg %job_id


kill

Sends a signal to a process, usually related to stopping the process.
All signals except for SIGKILL and SIGSTOP can be intercepted by the process to perform a clean exit.
More information: <https://manned.org/kill.1posix>.

- Terminate a program using the default SIGTERM (terminate) signal:
    kill process_id

- List available signal names (to be used without the `SIG` prefix):
    kill -l

- Terminate a program using the SIGHUP (hang up) signal. Many daemons will reload instead of terminating:
    kill -1|HUP process_id

- Terminate a program using the SIGINT (interrupt) signal. This is typically initiated by the user pressing `Ctrl + C`:
    kill -2|INT process_id

- Signal the operating system to immediately terminate a program (which gets no chance to capture the signal):
    kill -9|KILL process_id

- Signal the operating system to pause a program until a SIGCONT ("continue") signal is received:
    kill -17|STOP process_id

- Send a `SIGUSR1` signal to all processes with the given GID (group id):
    kill -SIGUSR1 -group_id
```


## Use Cases

- Display status of jobs in the current session
- Resume suspended jobs (e.g. using `Ctrl + Z`) and keep them running in the background
- Run jobs in foreground
- Send a signal to a process (e.g. send a signal to stop a process)


## References

- [jobs - manned.org](https://manned.org/jobs)
- [bg - manned.org](https://manned.org/bg)
- [fg - manned.org](https://manned.org/fg)
- [kill - manned.org](https://manned.org/kill.1posix)

