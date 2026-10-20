# Day 1 — Shell tools and scripting (Missing Semester, lecture 2)

My study summary of [Shell Tools and Scripting](https://missing.csail.mit.edu/2020/shell-tools/).

## 1. Variables

```bash
name=Youssef        # NO spaces around =
echo $name
echo "Hello $name"  # double quotes: variables ARE expanded  → Hello Youssef
echo 'Hello $name'  # single quotes: taken literally         → Hello $name
```

- `name = Youssef` fails: bash reads it as the command `name` with arguments `=` and `Youssef`.
- Rule of thumb: wrap variables in double quotes (`"$name"`) so spaces inside them don't split into several arguments.

## 2. Special variables

| Variable | Meaning |
| --- | --- |
| `$0` | Name of the script |
| `$1` … `$9` | Arguments passed to the script |
| `$@` | All arguments |
| `$#` | Number of arguments |
| `$?` | Exit code of the last command (`0` = success, anything else = error) |
| `$$` | Process ID of the current shell |
| `!!` | The whole last command (handy: `sudo !!`) |
| `$_` | Last argument of the last command |

```bash
ls /nope
echo $?    # non-zero → failed
ls /
echo $?    # 0 → success
```

## 3. Chaining commands

| Syntax | Runs the second command… |
| --- | --- |
| `a && b` | only if `a` **succeeded** |
| `a \|\| b` | only if `a` **failed** |
| `a ; b` | always |

```bash
mkdir demo && cd demo          # only cd if mkdir worked
grep foo file || echo "no foo" # message only if grep found nothing
```

## 4. Command substitution

`$( command )` runs the command and puts its **output** into the line.

```bash
echo "Today is $(date)"
files=$(ls)
echo "I am in $(pwd)"
```

(Advanced: `<( command )` — process substitution — turns output into a temporary file, e.g. `diff <(ls dir1) <(ls dir2)`.)

## 5. Tests and conditions

```bash
if [[ -f notes.txt ]]; then
  echo "file exists"
else
  echo "no file"
fi
```

Common tests: `-f` file exists, `-d` folder exists, `-z "$x"` string is empty, `"$a" == "$b"` strings equal, `$n -gt 5` number greater than. Use `[[ ]]` in bash (safer than `[ ]`). See `man test`.

## 6. Loops

```bash
for f in *.txt; do
  echo "Found $f"
done
```

## 7. Globbing (wildcards)

| Pattern | Matches |
| --- | --- |
| `*` | Any characters: `*.txt` → all .txt files |
| `?` | Exactly one character: `file?.txt` → `file1.txt`, not `file10.txt` |
| `{a,b}` | Expands to each option: `touch {a,b,c}.txt` → three files |
| `{1..5}` | A range: `mkdir day{1..5}` → five folders |

The **shell** expands these before the command runs — `ls` never sees the `*`.

## 8. Scripts and functions

```bash
#!/usr/bin/env bash
# greet.sh — say hello to every argument
for person in "$@"; do
  echo "Hello, $person"
done
```

- `#!/usr/bin/env bash` finds `bash` through `$PATH` — more portable than `#!/bin/bash`.
- Make it runnable: `chmod +x greet.sh`, then `./greet.sh Ali Sara`.
- **Functions** live in your current shell (they can `cd` and change variables there); a **script** runs in a new process, so its `cd` doesn't affect your shell.

```bash
mcd () {
  mkdir -p "$1"
  cd "$1"
}
```

- Load a file of functions into your current shell with `source file.sh`.
- Check scripts for bugs with **shellcheck**: `sudo apt install shellcheck`, then `shellcheck greet.sh`.

## 9. Finding things

| Need | Tool | Example |
| --- | --- | --- |
| How to use a command, quickly | `tldr` | `tldr tar` |
| Files by name | `find` | `find . -name "*.py"` |
| Folders only | `find` | `find . -type d -name src` |
| Recently changed files | `find` | `find . -mtime -1` (last day) |
| Text inside files | `grep` | `grep -R "TODO" .` |
| Text inside files, faster | `rg` (ripgrep) | `rg "TODO"` |

Useful `grep` flags: `-i` ignore case, `-R` search folders recursively, `-n` show line numbers, `-v` show lines that **don't** match.

## 10. Finding old commands

- `history` lists your past commands; `history | grep chmod` finds a specific one.
- **Ctrl+R** then type part of a command: searches history as you type. Press Ctrl+R again for older matches, Enter to run, Ctrl+C to cancel.
- **Tab** completes file and command names — use it constantly.

## 11. Getting around folders

- `tree` shows a folder as a tree (`sudo apt install tree`).
- `ls -lt` sorts by newest first; `ls -lh` shows sizes like `4.0K`.

## Exercises checklist

- [ ] Find the `ls` flags that: show hidden files, show sizes in human form (`454M`), sort by most recent, and use colours. Combine them in one command.
- [ ] Write two functions, `marco` and `polo`: `marco` saves the current folder, `polo` takes you back to it from anywhere.
- [ ] A command fails rarely. Write a script that runs it in a loop until it fails, saving its output and errors, and reports how many runs it took.
- [ ] Use `find` plus `xargs` to put every `.html` file in a folder (including subfolders, and names with spaces) into one zip.
- [ ] (Advanced) Find the most recently modified file in a folder tree.

## Test yourself

1. What's the difference between `"$name"` and `'$name'`?
2. What does `$?` hold after a successful command?
3. What's the difference between `&&` and `||`?
4. Who expands `*.txt` — the shell or `ls`?
5. Why can a function `cd` you into a folder, but a script can't?
