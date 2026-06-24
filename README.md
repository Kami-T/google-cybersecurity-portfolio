# Use Linux commands to manage file permissions

Portfolio project from the **Google Cybersecurity Professional Certificate** (course: *Tools of the Trade: Linux and SQL*). It documents how to audit and correct file and directory permissions in a Linux file system using the `ls` and `chmod` commands, applying the principle of least privilege.

## Scenario

Acting as a security professional supporting a research team, I was responsible for reviewing the permissions inside the `/home/researcher2/projects` directory. The goal was to determine whether the permissions granted to each owner type (user, group, and other) matched the authorization they should have, and to modify any permission that allowed unauthorized access — removing unauthorized access while keeping authorized users able to do their work.

## What was done

**1. Checked the current permissions**

```
ls -la
```

The `-l` flag shows the output in long format (including the 10-character permissions string, owner, and group), and the `-a` flag includes hidden files — those whose names begin with a period (`.`). This revealed the permissions of every file and directory in `projects`, including the hidden `.project_x.txt`.

**2. Removed write access from "other" on a file**

The organization does not allow *other* to have write access to any file. `project_k.txt` had the string `-rw-rw-rw-`, granting write to everyone, so it was corrected:

```
chmod o-w project_k.txt
```

**3. Fixed a hidden, archived file**

`.project_x.txt` was archived and should not be writable by anyone, but the user and group still need read access. Its original permissions (`-rw--w----`) gave the user write and the group write-only. Two changes were applied — remove write from user and group, and grant read to the group:

```
chmod u-w,g-w,g+r .project_x.txt
```

**4. Restricted a directory to its owner**

Only `researcher2` should access the `drafts` directory. The group still had execute access (`drwx--x---`), which for a directory is what allows entering it with `cd`. That access was removed:

```
chmod g-x drafts
```

## How to read a permissions string

A 10-character string such as `-rw-rw-r--` breaks down as:

- **char 1** — item type (`-` file, `d` directory)
- **chars 2-4** — **user** (owner) permissions
- **chars 5-7** — **group** permissions
- **chars 8-10** — **other** (everyone else) permissions

Within each group: `r` = read, `w` = write, `x` = execute, and `-` means the permission is not granted.

## Files in this repository

- [`01-linux-file-permissions/`](./01-linux-file-permissions) — full project folder
  - `File_permissions_in_Linux.docx` — the complete portfolio document with command explanations and terminal screenshots
  - `screenshots/` — terminal captures of the commands run in the lab

## Skills demonstrated

- Linux command line (`ls`, `chmod`)
- File and directory permission management
- Working with hidden files
- Principle of least privilege
- Security documentation
