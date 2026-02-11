# 🐧 Complete Bash Study Guide (Beginner to Practical)

This file is designed for **learning + revision + GitHub reference**.  
It covers essential Bash concepts with explanations and examples.

---

# 📌 1. What is Bash?

Bash (Bourne Again SHell) is a command-line interpreter used in:
- Linux
- macOS
- WSL (Windows Subsystem for Linux)
- DevOps & Cloud environments

It allows you to:
- Navigate files
- Manage directories
- Automate tasks
- Write scripts
- Control system processes

---

# 📂 2. File & Directory Commands

## 🔹 Check Current Directory
```bash
pwd
```
Prints your present working directory.

---

## 🔹 List Files
```bash
ls
```
Lists files and folders.

```bash
ls -la
```
Lists:
- Hidden files
- File permissions
- Owner
- Size
- Timestamp

---

## 🔹 Change Directory
```bash
cd folder_name
```

Go back:
```bash
cd ..
```

Go to home:
```bash
cd ~
```

---

## 🔹 Create Directory
```bash
mkdir folder_name
```

Safe creation (no error if exists):
```bash
mkdir -p folder_name
```

---

## 🔹 Create File
```bash
touch file.txt
```

---

## 🔹 Delete File
```bash
rm file.txt
```

---

## 🔹 Delete Folder
```bash
rm -r folder_name
```

⚠ Be careful with `rm -r`. It permanently deletes.

---

# 📜 3. Bash Scripts

## 🔹 Create Script
```bash
touch script.sh
```

---

## 🔹 Make Executable
```bash
chmod +x script.sh
```

---

## 🔹 Run Script
```bash
./script.sh
```

OR

```bash
bash script.sh
```

---

# 🔢 4. Variables & Arguments

## 🔹 Create Variable
```bash
VAR="Hello"
```

## 🔹 Use Variable
```bash
echo $VAR
```

---

## 🔹 Script Arguments

If script is run like:
```bash
./script.sh Ambuj
```

Inside script:
```bash
echo $1
```

Output:
```
Ambuj
```

---

## 🔹 Default Value
```bash
${1:-DEFAULT}
```

Uses `DEFAULT` if argument is empty.

---

# 🚦 5. Exit Codes

Every command returns a status code.

Check last exit code:
```bash
echo $?
```

Exit manually:
```bash
exit 0   # success
exit 1   # failure
```

### Rule:
- `0` → Success
- `Non-zero` → Error

Used heavily in automation & CI/CD.

---

# 🔍 6. Conditionals

## 🔹 Basic If Statement
```bash
if [ condition ]; then
  echo "True"
fi
```

---

## 🔹 File Exists
```bash
[ -f file.txt ]
```

---

## 🔹 Directory Exists
```bash
[ -d folder ]
```

---

## 🔹 Check Command Exists
```bash
command -v node
```

Useful in setup scripts.

---

# 🔄 7. Output Redirection

## 🔹 Overwrite Output
```bash
command > file.txt
```

---

## 🔹 Append Output
```bash
command >> file.txt
```

---

## 🔹 Discard Output
```bash
command > /dev/null
```

---

## 🔹 Discard Output + Errors
```bash
command > /dev/null 2>&1
```

Very useful in production scripts.

---

# ♻️ 8. Idempotent Operations

Idempotent means:
> Running multiple times gives same result.

Example:
```bash
[ -d logs ] || mkdir logs
```

Creates folder only if it doesn't exist.

---

# 🧠 9. Mini Practice Script

Create a file `setup.sh`:

```bash
#!/bin/bash

FOLDER="logs"

# Create folder if not exists
[ -d $FOLDER ] || mkdir $FOLDER

# Create file
touch $FOLDER/output.txt

# Write message
echo "Setup complete" > $FOLDER/output.txt

echo "Script finished successfully"
exit 0
```

Run:
```bash
chmod +x setup.sh
./setup.sh
```

---

# 🎯 10. Real-World Use Cases

Bash is used in:

- DevOps automation
- GitHub Actions
- CI/CD pipelines
- Server configuration
- Docker setup
- Cron jobs
- Deployment scripts

---

# ⚠️ Common Mistakes

❌ Forgetting quotes around variables  
❌ Using `rm -rf` carelessly  
❌ Not checking exit codes  
❌ Not making scripts executable  

---

# 🚀 Learning Roadmap

If you want to go deeper:

1. Loops (`for`, `while`)
2. Functions
3. Case statements
4. Process management
5. Cron jobs
6. Advanced piping
7. Writing deployment scripts

---

# 📌 Final Advice

- Practice in a test directory.
- Break scripts into small steps.
- Use `echo` for debugging.
- Understand exit codes clearly.
- Think in automation mindset.

---

# ✨ Summary

This guide covers:
- File management
- Scripts
- Variables
- Exit codes
- Conditions
- Redirection
- Idempotency

Master these → you're already ahead in DevOps & backend workflows.

---

Happy Learning 🚀
