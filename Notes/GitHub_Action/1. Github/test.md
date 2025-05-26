Bilkul bhai! Main `git rm`, `git restore`, aur `git log` ke baare mein detail mein samjhaata hoon, examples ke saath, taaki clearly samajh aaye.

---

## 🔹 `git rm` — **File ko Git se hataana (delete karna)**

### 📌 Kya karta hai:

`git rm` kisi file ko Git se hata deta hai **aur** working directory (yaani local folder) se bhi delete kar deta hai. Ye command staging area se bhi file hata deti hai, yaani commit karne ke liye file delete ho jaati hai.

### 🔧 Syntax:

```
git rm <file-name>
```

### 📂 Example:

Maan lo tumhare paas ek file hai `notes.txt`.

```bash
git rm notes.txt
git commit -m "Removed notes.txt"
```

Ab ye file Git repo se delete ho gayi hai, aur commit bhi ho gaya.

### ❗ Pro Tip:

Agar tum sirf Git se hataana chahte ho **lekin file ko system mein rakhna chahte ho**, to:

```bash
git rm --cached notes.txt
```

Ye file ko Git ke tracking se hata dega (useful in case of `.env` files ya koi bhi private file).

---

## 🔹 `git restore` — **Changes ko undo karna / restore karna**

### 📌 Kya karta hai:

`git restore` ka use tum apne file mein kiye gaye changes ko **revert** karne ke liye karte ho. Ye naye version ko hata kar purane committed version pe le jaata hai.

### 🔧 Syntax:

```bash
git restore <file-name>
```

### 📂 Example:

Tumne `index.html` file mein kuch changes kiye, lekin commit nahi kiya. Ab tum chahte ho ki file wapas original form mein aa jaaye:

```bash
git restore index.html
```

Ab file waise hi ho jaayegi jaise last commit mein thi.

### 🛑 Warning:

Isse tumhare recent (unsaved) changes chalayenge. So, use carefully!

---

## 🔹 `git log` — **Commit history dekhna**

### 📌 Kya karta hai:

`git log` tumhare Git repository ka **commit history** dikhata hai — kisne, kab, kya changes kiye.

### 🔧 Syntax:

```bash
git log
```

### 📂 Example Output:

```bash
commit 12a3f45d3e8c29d738e9c0
Author: Rahul <rahul@example.com>
Date:   Mon May 20 14:53:00 2025 +0530

    Added homepage content

commit b123a67de9a81c38f98a0b
Author: Rahul <rahul@example.com>
Date:   Sun May 19 13:40:00 2025 +0530

    Initial commit
```

### ✅ Extra Tips:

* Agar tum concise (short form) mein dekhna chahte ho:

  ```bash
  git log --oneline
  ```

* Agar tum kisi specific file ka log dekhna chahte ho:

  ```bash
  git log index.html
  ```

---

## 🔄 Ek Practical Flow:

```bash
echo "hello" > test.txt
git add test.txt
git commit -m "Add test.txt"

# Ab file ko hata do
git rm test.txt
git commit -m "Removed test.txt"

# Purana commit dekhna ho
git log

# Accidentally changes kar diye
git restore test.txt  # Agar file abhi tracked ho
```

---

Agar tum chaho to main ek chhota demo repo bana ke dikha sakta hoon step-by-step command ke sath. Bolo to shuru karte hain!
