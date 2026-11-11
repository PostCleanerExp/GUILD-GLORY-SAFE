# Push this source to the empty GitHub repository

The target repository is currently empty, so initialize the extracted project as its first commit.

```bash
cd /storage/emulated/0/Download
unzip -o GUILD-GLORY-SAFE-Render.zip
cd Guild_Glory_Bot

git init
git branch -M main
git add .
git commit -m "Prepare Guild Glory for Render 512MB"
git remote add origin https://github.com/PostCleanerExp/GUILD-GLORY-SAFE.git
git push -u origin main
```

Authenticate Git with your GitHub account first (for GitHub CLI users: `gh auth login` and `gh auth setup-git`). Do not add runtime files such as `accounts.json`, `accounts_archive.json`, `token_cache.json`, or `devices.json` to the repository.
