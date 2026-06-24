# Use Linux commands to manage file permissions

Portfolio project — **Google Cybersecurity Certificate** (Course: *Tools of the Trade: Linux and SQL*).

This project demonstrates how to audit and correct file and directory permissions in a Linux file system using the `ls` and `chmod` commands, applying the principle of least privilege.

## Scenario

As a security professional supporting a research team, I was responsible for reviewing the permissions inside the `/home/researcher2/projects` directory, determining whether each permission matched the authorization it should have, and modifying any that granted unauthorized access.

## Tasks performed

| # | Goal | Command |
|---|------|---------|
| 1 | Check permissions of all files and directories (including hidden) | `ls -la` |
| 2 | Remove write access from *other* on a file | `chmod o-w project_k.txt` |
| 3 | Fix permissions on a hidden, archived file (read for user/group, no write for anyone) | `chmod u-w,g-w,g+r .project_x.txt` |
| 4 | Restrict a directory so only the owner can access it | `chmod g-x drafts` |

## How to read a permissions string

A 10-character string such as `-rw-rw-r--` breaks down as:

- **1 char** — file type (`-` file, `d` directory)
- **chars 2-4** — user (owner) permissions
- **chars 5-7** — group permissions
- **chars 8-10** — other (everyone else) permissions

Within each group: `r` = read, `w` = write, `x` = execute, `-` = permission not granted.

## Files in this repository

- `File_permissions_in_Linux.docx` — the full portfolio document with command explanations and screenshots.
- `screenshots/` — terminal captures of the commands run in the lab.

## Skills demonstrated

- Linux command line (`ls`, `chmod`)
- File and directory permission management
- Principle of least privilege
- Security documentation
