# Linux Useful Commands

A short reference for common commands, redirection, and bash scripts.

## 1. Navigation & Files

| Command | What it does |
|---------|--------------|
| `pwd` | Print the current directory |
| `ls -la` | List files (long format, including hidden) |
| `cd /path` | Change directory |
| `mkdir name` | Create a directory |
| `touch file` | Create an empty file |
| `cp src dst` | Copy a file |
| `mv src dst` | Move or rename a file |
| `rm -r name` | Delete a file or directory |
| `find . -name "*.py"` | Find files by name |

## 2. Viewing & Editing

| Command | What it does |
|---------|--------------|
| `cat file` | Print a file's contents |
| `less file` | Scroll through a file |
| `head -20 file` | Show the first 20 lines |
| `tail -f file` | Follow a file (live logs) |
| `nano file` | Simple text editor |
| `grep "word" file` | Search for text in a file |

## 3. System & Processes

| Command | What it does |
|---------|--------------|
| `top` / `htop` | Live view of CPU and memory usage |
| `ps aux` | List all running processes |
| `kill PID` | Stop a process by its ID |
| `df -h` | Show disk usage |
| `free -h` | Show memory usage |
| `sudo cmd` | Run a command as root |
| `apt install pkg` | Install a package (Debian/Ubuntu) |

## 4. Pipes & Redirection

Two ideas that make the shell powerful:

- **`|` (pipe)** — sends the output of one command as input to another.

  ```bash
  ps aux | grep nginx     # find nginx processes
  ls -la | less           # scroll a long listing
  cat log | grep ERROR    # show only ERROR lines
  ```

- **`>` and `>>` (redirection)** — send output to a file instead of the screen.

  ```bash
  echo "hello" > file.txt   # overwrite file.txt
  echo "more" >> file.txt   # append to file.txt
  ls -la > listing.txt      # save a listing
  ```

## 5. Bash Scripts

A **bash script** is a plain text file containing a sequence of commands, run in order. Create a file (e.g. `backup.sh`):

```bash
#!/bin/bash
# A simple backup script
echo "Starting backup..."
mkdir -p ~/backups
cp -r ~/documents ~/backups/docs
echo "Done on $(date)" >> ~/backups/log.txt
```

Make it executable and run it:

```bash
chmod +x backup.sh
./backup.sh
```

Key points:

- The first line `#!/bin/bash` (the **shebang**) tells the system to run the file with bash.
- Each line is a command you could type manually — scripts simply automate sequences.
- Variables: `name="Patrice"` then use `$name`.
- Use `#` for comments.
