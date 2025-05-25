## Upload From Local To Git (New local folder to New repo) ----

```
PS D:\DevOps Notes\GitHubAction\new_code> git init 
Initialized empty Git repository in D:/DevOps Notes/GitHubAction/new_code/.git/
PS D:\DevOps Notes\GitHubAction\new_code> git add .
PS D:\DevOps Notes\GitHubAction\new_code> git commit -m "add readme"
[master (root-commit) f32bdc8] add readme
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 readme.md
PS D:\DevOps Notes\GitHubAction\new_code> git remote add origin https://github.com/dkchcl/test.git     
PS D:\DevOps Notes\GitHubAction\new_code> git branch -M main
PS D:\DevOps Notes\GitHubAction\new_code> git push -u origin main
Enumerating objects: 3, done.
Counting objects: 100% (3/3), done.
Writing objects: 100% (3/3), 204 bytes | 102.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)
To https://github.com/dkchcl/test.git
 * [new branch]      main -> main
branch 'main' set up to track 'origin/main'.
PS D:\DevOps Notes\GitHubAction\new_code> 
```
