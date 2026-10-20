# Day 1 — The shell (Missing Semester, lecture 1)

My study summary of [Course overview + the shell](https://missing.csail.mit.edu/2020/course-shell/).

## 1. What the shell is

- The shell is a program that reads a line of text, runs it, and prints the result. On Ubuntu it is **bash**.
- The prompt `youssef@youssef:~$` means: user `youssef`, machine `youssef`, current folder `~`, and `$` = normal user (`#` = root).
- A line is split on **spaces**: the first word is the **command**, the rest are **arguments**.
  - `cd ..` → command `cd`, argument `..` ✅
  - `cd..` → one word, no such command ❌
- Need a space inside one argument? Quote it: `mkdir "My Docs"` or escape it: `My\ Docs`.

## 2. How the shell finds commands: `$PATH`

- `$PATH` is a variable holding a list of folders separated by `:`.
- When you type `date`, the shell looks through those folders in order and runs the first `date` it finds.
- `which date` shows which file that is (e.g. `/usr/bin/date`).
- Variables are **case-sensitive**: `$PATH` works, `$path` is empty.

```bash
echo $PATH
which date
```

## 3. Paths

| Symbol | Meaning |
| --- | --- |
| `/` | The root: top of the whole filesystem |
| `~` | Your home folder (`/home/youssef`) |
| `.` | The current folder |
| `..` | The folder above (parent) |
| `-` (with `cd`) | The previous folder you were in |

- **Absolute path** starts with `/` and works from anywhere: `/home/youssef`.
- **Relative path** starts from where you are now: `youssef`, `../..`.
- `cd /youssef` fails because it means "youssef directly under `/`".

## 4. Moving around and managing files

| Command | Does | Example |
| --- | --- | --- |
| `pwd` | Print the current folder | `pwd` |
| `cd` | Change folder | `cd /tmp`, `cd ..`, `cd ~`, `cd -` |
| `ls` | List files | `ls`, `ls -l`, `ls -a` (show hidden `.files`) |
| `mkdir` | Make a folder | `mkdir /tmp/missing` |
| `touch` | Create an empty file (or update its time) | `touch notes.txt` |
| `cat` | Print a file | `cat notes.txt` |
| `cp` | Copy | `cp a.txt b.txt` |
| `mv` | Move or rename | `mv a.txt docs/` |
| `rm` | Delete a file (no recycle bin!) | `rm a.txt` |
| `rmdir` | Delete an empty folder | `rmdir docs` |

## 5. Getting help

- `man ls` — the full manual (move with arrows, search with `/word`, quit with `q`).
- `ls --help` — a short summary of options.
- Flags change behaviour: short `-l`, long `--all`. Short flags combine: `ls -la`.

## 6. Permissions (`ls -l`)

```
-rwxr-xr--  1 youssef youssef  220 Oct 18 18:49 script.sh
│└┬┘└┬┘└┬┘
│ │  │  └── everyone else: r-- (read only)
│ │  └───── group:          r-x (read, run)
│ └──────── owner:          rwx (read, write, run)
└────────── type: - file, d folder
```

- `r` read, `w` write, `x` execute. On a **folder**: `r` = list it, `w` = add/remove files in it, `x` = enter it (`cd`).
- `chmod +x script.sh` makes a file executable; then run it with `./script.sh`.

## 7. Streams: redirection and pipes

Every program has an **input** stream and an **output** stream (keyboard and screen by default).

| Symbol | Meaning | Example |
| --- | --- | --- |
| `>` | Send output to a file, **replacing** it | `echo hello > hello.txt` |
| `>>` | Send output to a file, **adding** to the end | `echo world >> hello.txt` |
| `<` | Read input from a file | `cat < hello.txt` |
| `\|` | Send output of the left command into the right one | `ls -l / \| tail -n 3` |

Pipes let you build big tools from small ones: each program does one job well.

## 8. Root and `sudo`

- `root` is the admin user and can do anything — including breaking the system.
- `sudo command` runs one command as root (asks for your password).
- **Gotcha:** `sudo echo 3 > /root-owned/file` fails. The `>` is done by *your* shell (as `youssef`) before `sudo` runs.
- **Fix:** let a root process do the writing:

```bash
echo 3 | sudo tee /root-owned/file
```

`tee` reads its input and writes it to the file (and the screen).

## Exercises checklist

- [ ] Create `/tmp/missing`
- [ ] Read `man touch`, then create `/tmp/missing/semester` with `touch`
- [ ] Write the two-line script into `semester` using `echo` and `>` / `>>` (watch the quotes!)
- [ ] Try to run `./semester` — why does it fail? Check `ls -l`
- [ ] Run it with `sh semester` — why does that work?
- [ ] Use `chmod` so `./semester` runs; explain what the `#!` line does
- [ ] Use `|` and `>` to save the "last modified" date from `semester` into `last-modified.txt`
- [ ] Write a command that reads a system value from `/sys` (laptop battery or similar; may not exist in WSL — that's fine, try `cat /sys/class/power_supply/*/capacity`)

## Test yourself

1. What is the difference between `/home` and `home`?
2. Why does `echo $path` print nothing?
3. What does `ls -la ~` show that `ls ~` doesn't?
4. What happens to a file's old contents with `>`? With `>>`?
5. Why does `sudo echo x > file` fail, and how does `tee` fix it?
