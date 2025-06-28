## Git command for Uploads files in Git Repo:


```
    git status
    git add .
    git status
    git restore --staged Infra/Prod/main.tf
    git status
    git add Infra/Prod/main.tf
    git status
    git commit -m "add all code"
   git status
   git restore --source HEAD~1 --staged Modules/nic/variable.tf
   git status
   git commit -m "add nic code"
   git status
   git push
   git status
   git checkout -b feature/test
   git branch
   git add .
   git status
   git commit -m "add readme"
   git push
   git push --set-upstream origin feature/test
   git status
```

## Git command ka detail mein explanation step-by-step:

---

### ✅ **1. `git status`**

**Purpose:** Git working directory aur staging area ka current status dikhata hai.

**Explanation:** Ye command batata hai ki kaunse files modified hain, staged hain ya untracked hain. Useful hota hai changes dekhne ke liye commit karne se pehle.

---

### ✅ **2. `git add .`**

**Purpose:** Saare modified aur untracked files ko staging area mein le jata hai.

**Explanation:** `.` ka matlab current directory aur uske andar ki sabhi files. Iska use karne ke baad, wo files next commit ke liye ready ho jaati hain.

---

### ✅ **3. `git status`**

**Purpose:** Fir se status check karte ho, taaki confirm ho jaaye ki files staging area mein aa gayi hain.

---

### ✅ **4. `git restore --staged Infra/Prod/main.tf`**

**Purpose:** Is command se `main.tf` file ko staging area se hata diya jaata hai, par working directory se nahi.

**Explanation:** Agar galti se koi file add ho gayi ho, to is command se usse staged se hata sakte hain bina file ko delete kiye.

---

### ✅ **5. `git status`**

**Purpose:** Check karte ho ki `main.tf` ab staged nahi hai.

---

### ✅ **6. `git add Infra/Prod/main.tf`**

**Purpose:** Dubara specifically `main.tf` ko staging area mein add karte ho.

**Reason:** Shayad ab sure ho ki ye file commit mein honi chahiye.

---

### ✅ **7. `git status`**

**Purpose:** Final confirmation ki ab sab sahi staged hai commit ke liye.

---

### ✅ **8. `git commit -m "add all code"`**

**Purpose:** Staged files ko commit karta hai aur message ke through describe karta hai ki commit mein kya changes kiye gaye.

---

### ✅ **9. `git status`**

**Purpose:** Ab koi pending staged changes nahi hai, working tree clean dikhayega.

---

### ✅ **10. `git restore --source HEAD~1 --staged Modules/nic/variable.tf`**

**Purpose:** Ye command `variable.tf` ko previous commit (`HEAD~1`) ki state mein staging area mein restore karta hai.

**Explanation:** Agar kisi specific file ka staged version pehle wale commit ke jaise rakhna ho, to aise karte hain.

---

### ✅ **11. `git status`**

**Purpose:** Check karne ke liye ki `Modules/nic/variable.tf` ka state ab change hua ya nahi.

---

### ✅ **12. `git commit -m "add nic code"`**

**Purpose:** Is commit mein specifically NIC module se related changes commit ho rahe hain.

---

### ✅ **13. `git status`**

**Purpose:** Confirm karta hai ki working directory clean hai ya nahi.

---

### ✅ **14. `git push`**

**Purpose:** Local commits ko remote repository (e.g., GitHub) par push karta hai.

---

### ✅ **15. `git status`**

**Purpose:** Fir se dekhte ho ki koi aur local changes to nahi bache.

---

### ✅ **16. `git checkout -b feature/test`**

**Purpose:** Nayi branch `feature/test` create karta hai aur turant usme switch bhi kar deta hai.

---

### ✅ **17. `git branch`**

**Purpose:** Dikhata hai ki ab kaunsi branch par ho aur kaunsi branches available hain.

---

### ✅ **18. `git add .`**

**Purpose:** Saari current changes ko staging area mein dal dete ho. Yahan shayad README add kiya gaya ho.

---

### ✅ **19. `git status`**

**Purpose:** Check karte ho ki kya changes staged hain commit ke liye.

---

### ✅ **20. `git commit -m "add readme"`**

**Purpose:** Staged changes (jaise README file) ko commit karte ho.

---

### ✅ **21. `git push`**

**Purpose:** Push karne ki koshish ki ja rahi hai, lekin nayi branch (`feature/test`) remote par abhi set nahi hai.

---

### ✅ **22. `git push --set-upstream origin feature/test`**

**Purpose:** Nayi branch ko remote origin par push karta hai aur uska upstream set karta hai, taki agle push/pull directly possible ho.

---

### ✅ **23. `git status`**

**Purpose:** Confirm karta hai ki ab koi local uncommitted changes to nahi hain.

---

## **step-by-step Git tutorial script** - project mein use karne ke liye:

---

## 🧠 **Git Command Script – Full Workflow**

```bash
# Step 1: Check current status of working directory and staging area
git status

# Step 2: Add all modified and untracked files to the staging area
git add .

# Step 3: Confirm what is staged
git status

# Step 4: Unstage a specific file (if added by mistake)
git restore --staged Infra/Prod/main.tf

# Step 5: Check that the file is no longer staged
git status

# Step 6: Add the correct version of the file back to staging
git add Infra/Prod/main.tf

# Step 7: Confirm all files staged properly
git status

# Step 8: Commit staged changes with a message
git commit -m "add all code"

# Step 9: Check clean working state
git status

# Step 10: Revert a specific file in staging to its previous commit version (HEAD~1)
git restore --source HEAD~1 --staged Modules/nic/variable.tf

# Step 11: Confirm the file is restored to earlier commit state
git status

# Step 12: Commit the NIC-related changes
git commit -m "add nic code"

# Step 13: Check status again
git status

# Step 14: Push all committed changes to remote repo
git push

# Step 15: Confirm nothing else is pending
git status

# Step 16: Create and switch to a new feature branch
git checkout -b feature/test

# Step 17: Check all available branches and current branch
git branch

# Step 18: Stage all changes (likely README or new files)
git add .

# Step 19: Confirm staging
git status

# Step 20: Commit the new files
git commit -m "add readme"

# Step 21: Try pushing (will fail if branch not set on remote yet)
git push

# Step 22: Push and set upstream tracking for the new branch
git push --set-upstream origin feature/test

# Step 23: Final check
git status
```

---

## 📁 Optional: Save as a Script File

You can save this as a `.sh` file (if you're using Linux/Mac) or `.bat` file (for Windows).
Example:

```bash
nano git-workflow.sh
```

Then paste the above script and save.

---

## ✅ Tips:

* Use `git log --oneline` to see commit history.
* Use `git diff` to see actual code differences before committing.
* Keep commit messages meaningful.

---

Kuch aur bhi Git se related chahiye ho jaise `git rebase`, `merge`, `stash`, ya `conflict resolve` tutorial to bata dena bhai. 💻
