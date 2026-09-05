# Linux Learning

## Table of Contents
1. [Terminal Basics](#1-Terminal-Basics)

## 1.Terminal Basics

A hands-on reference covering the Linux command-line concepts and commands I have learned so far.

The focus is on understanding what each command does, practicing it in the terminal, and gradually combining commands to solve practical problems.

---

## 1. Terminal basics

The terminal provides a text-based interface for interacting with the operating system.

Instead of using a graphical interface, commands can be used to navigate directories, create and manipulate files, inspect information, and process data.

### Useful basic commands

| Command    | Purpose                                      |
| ---------- | -------------------------------------------- |
| `pwd`      | Displays the current working directory       |
| `whoami`   | Displays the current username                |
| `hostname` | Displays the system's hostname               |
| `clear`    | Clears the terminal screen                   |
| `history`  | Displays previously executed commands        |
| `man`      | Opens the manual/documentation for a command |

Example:

```bash
pwd
```

Output might look like:

```text
/home/user
```

---

# 2. Directory Navigation

Navigation commands are used to move around the filesystem.

### `cd`

Moves to a specified directory.

```bash
cd documents
```

### `cd ..`

Moves one level up to the parent directory.

```bash
cd ..
```

For example:

```text
/home/user/documents
        ↑
     cd ..
        ↓
/home/user
```

### `cd ~`

Moves to the user's home directory.

```bash
cd ~
```

### `cd -`

Returns to the previous directory.

```bash
cd -
```

This is useful when switching between two directories.

---

# 3. Listing Files and Directories

### `ls`

Displays files and directories in the current directory.

```bash
ls
```

### `ls -l`

Displays files in a detailed/list format.

```bash
ls -l
```

### `ls -la`

Displays detailed information including hidden files.

```bash
ls -la
```

---

# 4. Creating Files and Directories

## `touch`

Creates an empty file.

```bash
touch notes.txt
```

If the file already exists, `touch` updates its timestamp instead of creating another file.

---

## `mkdir`

Creates a directory.

```bash
mkdir documents
```

Example:

```bash
mkdir backups
```

---

# 5. Writing Content to Files

## `echo`

Used to print text, and when combined with redirection, write text into a file.

```bash
echo "Hello World" > file.txt
```

---

## `>`

Writes output to a file and **overwrites existing content**.

```bash
echo "First line" > file.txt
```

If `file.txt` already contained data, that data will be replaced.

---

## `>>`

Appends output to the end of a file without removing existing content.

```bash
echo "Second line" >> file.txt
```

For example:

```bash
echo "Hello" > file.txt
echo "World" >> file.txt
```

The file becomes:

```text
Hello
World
```

---

# 6. Copying and Moving Files

## `cp`

Copies a file or directory.

### Syntax

```bash
cp source destination
```

Example:

```bash
cp notes.txt backup.txt
```

This produces:

```text
notes.txt
backup.txt
```

The original file remains.

### Copy into a directory

```bash
cp notes.txt backups/
```

### Copy a directory

```bash
cp -r documents/ backups/
```

`-r` means recursively copy the directory and its contents.

---

# 7. Moving and Renaming Files

## `mv`

Moves a file or directory.

```bash
mv notes.txt documents/
```

The file is moved from its original location into `documents`.

### `mv` can also rename files

```bash
mv notes.txt important_notes.txt
```

This does not create a second file. It changes the name of the original file.

### `cp` vs `mv`

```text
cp
 ↓
Creates a copy
 ↓
Original remains
```

```text
mv
 ↓
Moves or renames the original
 ↓
No duplicate is created
```

---

# 8. Deleting Files and Directories

## `rm`

Deletes files.

```bash
rm file.txt
```

It can also remove directories when used with appropriate options.

---

## `rmdir`

Removes an **empty directory**.

```bash
rmdir old_directory
```

If the directory contains files, `rmdir` will not remove it.

---

# 9. Viewing File Contents

## `cat`

Displays the contents of a file.

```bash
cat notes.txt
```

It is useful for quickly viewing small files.

---

## `less`

Allows you to view a file interactively, especially useful for large files.

```bash
less large_file.txt
```

Useful keys inside `less`:

| Key     | Action             |
| ------- | ------------------ |
| `Space` | Next page          |
| `b`     | Previous page      |
| `↑`     | Move up            |
| `↓`     | Move down          |
| `/word` | Search for a word  |
| `n`     | Next search result |
| `q`     | Quit `less`        |

To exit:

```text
q
```

---

## `head`

Displays the beginning of a file.

```bash
head file.txt
```

Useful for quickly inspecting the first few lines.

---

## `tail`

Displays the end of a file.

```bash
tail file.txt
```

Useful when you want to inspect the most recent/end portion of a file.

---

## `file`

Identifies the type of a file based on its contents.

```bash
file example.txt
```

The command does not simply trust the file extension; it examines the file to determine its type.

---

# 10. Searching and Filtering

## `grep`

Searches for matching text inside files or command output.

Example:

```bash
grep "LOGIN_FAILED" auth.log
```

This displays lines containing:

```text
LOGIN_FAILED
```

This is particularly useful when working with logs.

---

# 11. Extracting Fields with `awk`

`awk` can process structured text and extract specific fields.

Example:

```bash
grep "LOGIN_FAILED" auth.log | awk '{print $1}'
```

If the input is:

```text
192.168.1.20 LOGIN_FAILED
192.168.1.10 LOGIN_FAILED
192.168.1.30 LOGIN_FAILED
```

`$1` represents the first field, so the output becomes:

```text
192.168.1.20
192.168.1.10
192.168.1.30
```

---

# 12. Sorting Data

## `sort`

Arranges lines in order.

```bash
sort users.txt
```

---

## `sort -nr`

Sorts numbers in **reverse numerical order**.

Breakdown:

```text
sort
 ↓
Sort the lines

-n
 ↓
Treat values as numbers

-r
 ↓
Reverse the order
```

Example:

```bash
echo -e "5\n2\n10\n1" | sort -nr
```

Output:

```text
10
5
2
1
```

---

# 13. Counting Duplicate Values

## `uniq -c`

Counts consecutive identical lines.

Example:

```bash
sort users.txt | uniq -c
```

If the data is:

```text
admin
admin
root
root
root
user
```

The result is approximately:

```text
2 admin
3 root
1 user
```

`sort` is commonly used before `uniq -c` because `uniq` counts adjacent duplicate lines.

---

# 14. Counting Lines

## `wc -l`

Counts the number of lines.

Example:

```bash
cat users.txt | wc -l
```

If the file contains 6 lines:

```text
6
```

---

# 15. Pipes

The pipe operator:

```text
|
```

connects commands together.

The output of one command becomes the input of the next command.

Basic idea:

```text
COMMAND 1
    ↓
  output
    ↓
    |
    ↓
COMMAND 2
```

Example:

```bash
cat users.txt | wc -l
```

Here:

```text
cat users.txt
      ↓
produces file contents
      ↓
      |
      ↓
wc -l
      ↓
counts the lines
```

Pipes become powerful when several commands are chained together.

---

# 16. Practical Example — Investigating Failed Logins

Consider this fake authentication log:

```text
192.168.1.10 LOGIN_SUCCESS
192.168.1.20 LOGIN_FAILED
192.168.1.10 LOGIN_FAILED
192.168.1.30 LOGIN_FAILED
192.168.1.20 LOGIN_SUCCESS
192.168.1.30 LOGIN_FAILED
```

### Step 1 — Find failed logins

```bash
grep "LOGIN_FAILED" auth.log
```

Result:

```text
192.168.1.20 LOGIN_FAILED
192.168.1.10 LOGIN_FAILED
192.168.1.30 LOGIN_FAILED
192.168.1.30 LOGIN_FAILED
```

### Step 2 — Extract the IP addresses

```bash
grep "LOGIN_FAILED" auth.log | awk '{print $1}'
```

Result:

```text
192.168.1.20
192.168.1.10
192.168.1.30
192.168.1.30
```

### Step 3 — Count each IP

```bash
grep "LOGIN_FAILED" auth.log | awk '{print $1}' | sort | uniq -c
```

Result:

```text
1 192.168.1.10
1 192.168.1.20
2 192.168.1.30
```

### Step 4 — Find the most frequent IP

```bash
grep "LOGIN_FAILED" auth.log | awk '{print $1}' | sort | uniq -c | sort -nr
```

Result:

```text
2 192.168.1.30
1 192.168.1.20
1 192.168.1.10
```

Therefore:

```text
192.168.1.30 → 2 failed login attempts
```

---

# 17. Understanding the Pipeline

The complete command:

```bash
grep "LOGIN_FAILED" auth.log | awk '{print $1}' | sort | uniq -c | sort -nr
```

can be understood as:

```text
grep
 ↓
Find failed logins

awk
 ↓
Extract IP addresses

sort
 ↓
Put identical IPs together

uniq -c
 ↓
Count each IP

sort -nr
 ↓
Put highest count first
```

The important concept is that **each command performs one small operation**, and the pipe connects those operations into a larger workflow.

---

# 18. Hands-On Exercises

## Exercise 1 — Directory Structure

Create:

```text
terminal_lab/
├── documents/
├── logs/
├── scripts/
└── backups/
```

Commands to practice:

```bash
mkdir
cd
ls
pwd
```

---

## Exercise 2 — File Manipulation

Inside `documents`, create:

```text
notes.txt
passwords.txt
report.txt
```

Then:

1. Copy `notes.txt` into `backups`.
2. Rename `report.txt` to `final_report.txt`.
3. Move `passwords.txt` into `backups`.
4. Delete a test file using `rm`.
5. Verify the final structure using `ls`.

---

## Exercise 3 — Pipes

Create:

```bash
printf "admin\nuser\nroot\nguest\nadmin\nroot\n" > users.txt
```

Then practice:

1. Display the contents.
2. Count the lines.
3. Find only `root`.
4. Count how many times `admin` appears.
5. Sort the usernames.
6. Remove duplicates.

Commands to investigate:

```text
cat
grep
wc
sort
uniq
|
```

---

# 19. Cybersecurity Mini-Lab

Create:

```bash
mkdir cyber_lab
cd cyber_lab
```

Create a fake authentication log:

```bash
printf "192.168.1.10 LOGIN_SUCCESS\n192.168.1.20 LOGIN_FAILED\n192.168.1.10 LOGIN_FAILED\n192.168.1.30 LOGIN_FAILED\n192.168.1.20 LOGIN_SUCCESS\n192.168.1.30 LOGIN_FAILED\n" > auth.log
```

### Investigation tasks

1. Display the log.
2. Find failed login attempts.
3. Extract the IP addresses.
4. Count failed login attempts.
5. Determine which IP appears most frequently.
6. Save the findings into:

```text
reports/failed_logins.txt
```

7. Create a backup of the report.

This exercise combines:

```text
File creation
     ↓
File viewing
     ↓
grep
     ↓
awk
     ↓
Pipes
     ↓
sort
     ↓
uniq
     ↓
Redirection
     ↓
File manipulation
```

---

# 20. Key Concepts Learned

The most important concepts from this section are:

### Filesystem navigation

```text
pwd
ls
cd
```

### File manipulation

```text
touch
mkdir
cp
mv
rm
rmdir
```

### File inspection

```text
cat
less
head
tail
file
```

### Text processing

```text
grep
awk
sort
uniq
wc
```

### Command combination

```text
|
>
>>
```

The larger lesson is that Linux commands are designed to be **combined**. Rather than looking for one command that performs an entire task, you can chain smaller commands together.

---

