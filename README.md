# 🕹️ OverTheWire — Bandit Level 3 → Level 4

In this lab I located the password for **Bandit Level 4**, which is hidden inside a dot-file in the `inhere` directory. I used `ssh` to connect on the non-standard port, inspected the directory (including hidden files), and read the hidden file to retrieve the password — then saved it to my notes.

📋 Lab Overview

**Goal:**
Find the password for the next level (stored in a hidden file inside the `inhere` directory).

**Why this matters:**
Teaches how to reveal hidden files on a Unix filesystem (`ls -a`) and how to safely read dot-files.

**Learning outcomes:**

* Use `ssh -p` to connect on a non-standard port.
* Understand hidden files (those beginning with `.`) and how to list them.
* Use `cat` (or similar) to read the hidden file containing the password.
* Save credentials securely in notes.

---

🛠 Step-by-Step Journey

**Step 1 — SSH into the host (non-standard port)**
Task: Connect to the Bandit server as `bandit3` on port `2220`.
Command:

```bash
ssh -p 2220 bandit3@bandit.labs.overthewire.org
```

Result: Logged in using the password from the previous level.

**Step 2 — Confirm location & list files**
Task: Check working directory and list files.

```bash
pwd
# Output:
# /home/bandit3

ls
# Output:
# (no obvious file containing the password)
```

**Step 3 — Reveal hidden files**
Task: List *all* files (including dot-files) inside the directory you were pointed to (`inhere`).

```bash
cd inhere
ls -a
# Output example (you will see dot-files listed):
# .  ..  .hidden-file-name  some_other_file
```

Observation: `ls -a` revealed a hidden dot-file whose name contained the password.

**Step 4 — Read the hidden file**
Task: Use `cat` (pointing to the exact dot-file name shown by `ls -a`) to print the password.

```bash
cat .hidden-file-name
# Output:
# (a single line string — the password for the next level)
```

Result: The command printed the password for **Level 4**. I copied it into my notes and exited the session.

**Step 5 — Exit**

```bash
exit
# logout
# Connection to bandit.labs.overtherewire.org closed.
```

---

🧾 Terminal session (concise example using placeholders)

```bash
bandit3@bandit:~$ pwd
/home/bandit3

bandit3@bandit:~$ ls
# (no visible file containing the password)

bandit3@bandit:~$ cd inhere

bandit3@bandit:~/inhere$ ls -a
.  ..  .hidden-file-name  maybe-some-other-file

bandit3@bandit:~/inhere$ cat .hidden-file-name
<password-for-bandit4>
# (copy the password into notes)

bandit3@bandit:~/inhere$ exit
logout
Connection to bandit.labs.overthewire.org closed.
```

---

✅ Key Commands Summary

| Task                                 | Command                                           |
| ------------------------------------ | ------------------------------------------------- |
| SSH to bandit host on port 2220      | `ssh -p 2220 bandit3@bandit.labs.overthewire.org` |
| Print working directory              | `pwd`                                             |
| List visible files                   | `ls`                                              |
| List all files (including dot-files) | `ls -a`                                           |
| Change directory                     | `cd inhere`                                       |
| Read a file                          | `cat .hidden-file-name`                           |
| Exit session                         | `exit`                                            |

💡 Notes / Tips

* Hidden files start with a dot (`.`). `ls` does **not** show them by default — use `ls -a`.
* Always use the filename exactly as shown by `ls -a` when running `cat`. Quoting is only necessary if the name contains spaces (rare for dot-files in these levels).
* Save found passwords immediately to a secure notes file (don't leave them only in terminal history).
* If `cat` fails due to permissions, check `ls -l` to inspect mode bits; for Bandit levels the files are usually world-readable.

✅ References

* OverTheWire — Bandit wargame (level instructions).
* `ls` and `cat` man pages (`man ls`, `man cat`) — listing and reading files on Unix.

---

🏁 End of Lab — Level cleared.
Password retrieved and saved to notes; ready to SSH into the next level.
