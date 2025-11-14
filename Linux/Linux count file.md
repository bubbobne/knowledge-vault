---
owner: Daniele Andreis
created: November 08, 2025 – 8:43 AM
updated: 2025-11-08
tags: [linux, console]
---
# Linux count file

Owner: Daniele Andreis
Last edited time: June 18, 2025 12:29 PM
Created time: June 18, 2025 12:29 PM

🕓 **[2025-05-26 14:18]**

**Confidence: 100/100**

Ottima richiesta! Ti propongo una **guida pratica e copincollabile in Notion**, con una raccolta di **comandi utili per lavorare con tanti file in una cartella** (anche migliaia), con attenzione alle performance e al caso d'uso.

---

### 🔧 Linux File Operations – Daily Use Cases

---

### ✅ **1. Count all files in a folder**

```bash
ls -1 | wc -l

```

🔹 Counts only files and folders (not recursive).

Alternative (recursive):

```bash
find . -type f | wc -l

```

---

### ✅ **2. Count files by extension**

```bash
find . -type f -name "*.jpg" | wc -l

```

🔹 Replace `*.jpg` with any extension you want.

---

### ✅ **3. List files ordered by modification date (most recent first)**

```bash
ls -lt

```

🔹 Only names:

```bash
ls -lt | head

```

🔹 Include hidden files:

```bash
ls -lat

```

---

### ✅ **4. List newest file only**

```bash
ls -t | head -n 1

```

---

### ✅ **5. List oldest file**

```bash
ls -tr | head -n 1

```

---

### ✅ **6. When there are thousands of files**

- 📌 **Avoid `ls` alone**, it's inefficient.
- Use `find` + `head` or `tail`:

```bash
find . -maxdepth 1 -type f -printf '%T@ %p\n' | sort -n | tail -n 10

```

🔹 Shows **10 most recently modified files** (fast even with 10k+ files).

---

### ✅ **7. Show file size in human readable format**

```bash
du -sh *

```

🔹 For folders too.

If you want only files:

```bash
find . -maxdepth 1 -type f -exec du -h {} + | sort -h

```

---

### ✅ **8. Show total size of all files**

```bash
du -sh .

```

---

### ✅ **9. Remove files older than 30 days**

```bash
find . -type f -mtime +30 -delete

```

🛑 Always test first:

```bash
find . -type f -mtime +30

```

---

### 🧠 Extra: When working with logs or large datasets

- **Tail last 100 lines of the newest log:**

```bash
ls -t *.log | head -n 1 | xargs tail -n 100

```

- **Watch for new files being written:**

```bash
watch "ls -lt | head"

```

---

### 🧪 Suggestion for automation

If you frequently work with these, create aliases or scripts. Example:

```bash
alias countjpg='find . -type f -name "*.jpg" | wc -l'

```

---