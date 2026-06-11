# 🛡️ Let's Learn Linux — Episode 1

**ParoCyber DevSecOps Bootcamp | CypherCore Systems Field Assignment**
**Trainee:** Providence Annor Asemah
**Submitted:** June 2026

---

## What This Is

This repository is my documented submission for **Let's Learn Linux — Episode 1**, a field assignment from the ParoCyber DevSecOps Bootcamp facilitated by Samuel Nartey.

The assignment follows a day in the life of Providence Mensah, a Junior DevSecOps Trainee at CypherCore Systems. Rather than being handed commands to copy, I had to figure out the right tool for each task, execute it, and — most importantly — explain *why* it works.

---

## What I Built

A full simulated DevSecOps environment from scratch, including:

- A production-style directory structure for a client pipeline (`configs/`, `logs/`, `reports/`, `archive/`)
- Simulated application logs written with `echo` and heredoc notation
- Archived and date-stamped log files using `cp` and `mv`
- Hard links and symbolic links — with experiments showing what happens at the inode level when originals are deleted
- Separated stdout and stderr streams into distinct files
- A weekly security report written in a single heredoc operation

---

## Repository Structure

```
lets-learn-linux-1/
├── answers.md          ← Full written answers to Q1–Q21
├── screenshots/        ← Terminal screenshots for every execute task
│   ├── q1.png
│   ├── q4_tree.png
│   ├── q7_tree.png
│   ├── q8.png
│   ├── q10_heredoc.png
│   ├── q12.png
│   ├── q14_tree.png
│   ├── q15.png
│   ├── q16.png
│   ├── q17.png
│   ├── q19.png
│   ├── q20.png
│   └── q21_tree.png
└── README.md
```

---

## Sections Covered

| Section | Topic | Marks |
|---------|-------|-------|
| Section 1 | Orient Yourself — `pwd`, `whoami`, `uname -a`, FHS, hidden files | 10 |
| Section 2 | Build the Environment — `mkdir -p`, brace expansion, `touch`, `tree` | 15 |
| Section 3 | Write and Read Files — `echo`, `>>`, heredoc, `cat`, `tac`, `less`, `more` | 20 |
| Section 4 | Move and Clean Up — `cp`, `mv`, `rmdir`, `rm -r` | 10 |
| Section 5 | Links and Inodes — hard links, symlinks, inode numbers, dangling links | 20 |
| Section 6 | Data Streams and Redirection — stdin/stdout/stderr, `2>`, `2>&1` | 15 |

---

## Key Things I Learned

**Inodes changed everything.** Before this lab, a file was just a name. After running `ls -li` and watching `db.conf` and `db_hardlink.conf` share the same inode number, the abstraction became real — a filename is just a pointer, and data exists independently of what it's called.

**`2>&1` finally made sense.** I had copy-pasted this in scripts without understanding it. Learning that stdout and stderr are numbered file descriptors, and that `2>&1` redirects one to the other's current destination, explains every "disappeared error" I've seen in CI/CD pipelines.

**`>>` vs `>` is not a typo — it's a data loss event.** In a production log rotation script, confusing these two operators silently destroys the log content with exit code 0 and no error message.

---

## How to Reproduce

All commands were run on Ubuntu 24.04 LTS. To reproduce the environment:

```bash
# Clone the repo
git clone https://github.com/YOUR_USERNAME/lets-learn-linux-1.git
cd lets-learn-linux-1

# Rebuild the directory structure
mkdir -p ~/projects/cyphercore/{configs,logs/{access,errors,archive},reports}

# Create placeholder files
touch ~/projects/cyphercore/configs/app.conf \
      ~/projects/cyphercore/configs/db.conf \
      ~/projects/cyphercore/logs/access/access.log \
      ~/projects/cyphercore/logs/errors/error.log \
      ~/projects/cyphercore/reports/weekly_report.txt
```

From there, follow `answers.md` section by section — each command is documented with its output and explanation.

---

## About the Bootcamp

This assignment is part of the DevSecOps training organised by **@ParoCyber** and facilitated by **Samuel Nartey**.

> *"You don't need to memorise every command. You need to understand why each one exists — because on a live server at 2 AM, there's no Google."*
> — Samuel Nartey, Lead Facilitator
