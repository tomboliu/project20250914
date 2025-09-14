project20250914
===

1. 檢查工具版本
```bash
git --version
gh --version
```
```output
git version 2.39.5
gh version 2.78.0 (2025-08-21)
https://github.com/cli/cli/releases/tag/v2.78.0
```

2. 地端登入 GitHub
```bash
gh auth login
```
```output
? Where do you use GitHub? GitHub.com
? What is your preferred protocol for Git operations on this host? HTTPS
? How would you like to authenticate GitHub CLI? Login with a web browser

! First copy your one-time code: 9EFC-1B8A
Press Enter to open https://github.com/login/device in your browser...
```

3. 檢查登入
> 登入憑證資訊會存在 ~/.config/gh/hosts.yml
```bash
cat ~/.config/gh/hosts.yml
```
```output
github.com:
    略 (GitHub 禁止有驗證資訊)
    user: tomboliu
    git_protocol: https
    users:
        tomboliu:
            略 (GitHub 禁止有驗證資訊)
```
> 可以用指令檢查登入的資訊及權限
```bash
gh auth status
```
```output
github.com
  ✓ Logged in to github.com account tomboliu (/home/pi/.config/gh/hosts.yml)
  - Active account: true
  - Git operations protocol: ssh
  - Token: ghp_*************************************
  - Token scopes: 'admin:enterprise', 'admin:gpg_key', 'admin:org', 'admin:org_hook', 'admin:public_key', 'admin:repo_hook', 'admin:ssh_signing_key', 'audit_log', 'codespace', 'copilot', 'delete:packages', 'delete_repo', 'gist', 'notifications', 'project', 'repo', 'user', 'workflow', 'write:discussion', 'write:packages'
```

4. 初始化 Repository/Project
```bash
git init
```
```output
hint: Using 'master' as the name for the initial branch. This default branch name
hint: is subject to change. To configure the initial branch name to use in all
hint: of your new repositories, which will suppress this warning, call:
hint:
hint:   git config --global init.defaultBranch <name>
hint:
hint: Names commonly chosen instead of 'master' are 'main', 'trunk' and
hint: 'development'. The just-created branch can be renamed via this command:
hint:
hint:   git branch -m <name>
Initialized empty Git repository in /home/pi/Desktop/project20250914/.git/
```
```bash
git config --global user.name tomboliu
git config --global user.email tomliu6116@hotmail.com
git config --global init.defaultBranch main
git branch -m main
```

5. 產生一個 README.md
> 在 GitHub/Gitlab 有些特定檔案名稱，有特定功能，大小寫必須一樣
```bash
echo "# project20250914" >> README.md
git add README.md
git commit -m "Initial commit"
```
```output
[main (root-commit) 2d46494] Initial commit
 1 file changed, 1 insertion(+)
 create mode 100644 README.md
```
> 為什麼要產生這個 README.md ?
> 1. 沒有 commit，不准 Push
> 2. 沒有 檔案檔案異動，不准 Commit

6. 地端透過指令建立GitHub Repository project20250914
```bash
gh repo create project20250914 --public --source=. --remote=origin --push
```
```output
✓ Created repository tomboliu/project20250914 on github.com
  https://github.com/tomboliu/project20250914
✓ Added remote git@github.com:tomboliu/project20250914.git
The authenticity of host 'github.com (20.27.177.113)' can't be established.
ED25519 key fingerprint is SHA256:+DiY3wvvV6TuJJhbpZisF/zLDA0zPMSvHdkr4UvCOqU.
This key is not known by any other names.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added 'github.com' (ED25519) to the list of known hosts.
Enumerating objects: 3, done.
Counting objects: 100% (3/3), done.
Writing objects: 100% (3/3), 233 bytes | 233.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
To github.com:tomboliu/project20250914.git
 * [new branch]      HEAD -> main
branch 'main' set up to track 'origin/main'.
✓ Pushed commits to git@github.com:tomboliu/project20250914.git
```

7. 檢查 Push 後的資訊
```bash
git log --oneline
```
```output
f019ee2 (HEAD -> main, origin/main) Initial commit with clean README
2d46494 Initial commit
```

8. 檢查地端專案資訊
```bash
git config --list
```
```output
user.email=tomliu6116@hotmail.com
user.name=Tom Liu
init.defaultbranch=main
core.repositoryformatversion=0
core.filemode=true
core.bare=false
core.logallrefupdates=true
remote.origin.url=git@github.com:tomboliu/project20250914.git
remote.origin.fetch=+refs/heads/*:refs/remotes/origin/*
branch.main.remote=origin
branch.main.merge=refs/heads/main
```

9. 檢查 Repository 狀態
```bash
git status
```
```output
On branch main
Your branch is up to date with 'origin/main'.

nothing to commit, working tree clean
```

99. 補充說明

```bash
# 將檔案從 staging area 移除，等 commit 時，會刪除此檔案
git rm --cache README.md
# 將檔案從 staging area 移除，等 commit 時，不會刪除此檔案
git restore --staged README.md
```

> nl -ba README.md | sed -n '30,45p' <br/>
> git reset --soft HEAD~1 <br/>
> git add README.md <br/>
> git commit -m "Initial commit with clean README" <br/>


<br/>
<br/>
<br/>
<br/>
<br/>
