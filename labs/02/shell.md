# Lab 2 · My shell

System: macOS, Terminal app. User name replaced with `<user>`.

## Task 1 · Get to know my shell

### 1. Which shell?

```bash
echo $0
zsh --version
```

```text
-zsh
zsh 5.9 (arm64-apple-darwin25.0)
```

My terminal runs zsh, version 5.9; the `-` in front of `zsh` means it is a login shell.

### 2. Where am I?

```bash
cd ~
pwd
cd ~/Downloads
pwd
```

```text
/Users/<user>
/Users/<user>/Downloads
```

My home directory is `/Users/<user>`, and my downloads folder is `/Users/<user>/Downloads`.

### 3. Where do commands come from?

```bash
echo $PATH | tr ":" "\n" | wc -l
echo $PATH | tr ":" "\n" | head -n 1
which curl python3 git
git --version
```

```text
      13
/opt/miniconda3/bin
/usr/bin/curl
/opt/miniconda3/bin/python3
/usr/bin/git
git version 2.50.1 (Apple Git-155)
```

My `PATH` has 13 directories, and Miniconda's `/opt/miniconda3/bin` is searched first, so `python3` comes from Miniconda, while `curl` and `git` (version 2.50.1) come from the system in `/usr/bin`.

### 4. How full is my disk?

```bash
df -h ~
du -sh ~/Downloads
```

```text
Filesystem      Size    Used   Avail Capacity iused ifree %iused  Mounted on
/dev/disk3s5   228Gi   190Gi    15Gi    93%    1,0M  158M    1%   /System/Volumes/Data
2,5G    /Users/<user>/Downloads
```

15 GiB of 228 GiB are free and my downloads take up 2.5 GB; the macOS settings show 69 GB free of 245 GB instead, because they count in GB instead of GiB and count space that macOS can free automatically (caches, local snapshots) as free.

At first, `du` failed with `Operation not permitted`: macOS blocks the Terminal from the downloads folder until you allow it under *System Settings → Privacy & Security → Files and Folders*.

### 5. Stop a runaway process

Window 1:

```bash
sleep 600
```

Window 2:

```bash
ps aux | grep sleep
kill 39921
```

```text
<user>  39935   0,0  0,0 435234128   1024 s001  R+    3:50   0:00.01 grep sleep
<user>  39921   0,0  0,0 435234032   1088 s000  S+    3:50   0:00.01 sleep 600
```

Window 1 afterwards:

```text
zsh: terminated  sleep 600
```

The first window shows `zsh: terminated  sleep 600`; `ps aux | grep sleep` lists two processes because the `grep sleep` command contains the word *sleep* itself and therefore finds its own process.

## Task 2 · bashcrawl

…
