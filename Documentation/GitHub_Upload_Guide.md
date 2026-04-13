# 🚀 GitHub Upload Guide - Complete Instructions

## 📋 What You Need

### Requirements:
1. ✅ Git installed ([Download](https://git-scm.com/downloads))
2. ✅ GitHub account ([Sign up](https://github.com/signup))
3. ✅ All project files ready

---

## 🎯 STEP 1: Install Git (if you don't have it)

### Windows:
1. Download Git from https://git-scm.com/downloads
2. Install with default options
3. Open **Git Bash** (Right-click → Git Bash Here)

### Verify installation:
```bash
git --version
# Output: git version 2.43.0 (or similar)
```

---

## 👤 STEP 2: Configure Git (first time only)

```bash
# Set your name
git config --global user.name "Nikola Kotlaja"

# Set your email (use same as GitHub)
git config --global user.email "your.email@example.com"

# Verify configuration
git config --list
```

---

## 📁 STEP 3: Navigate to Project

```bash
# Windows (Git Bash)
cd /c/Users/YourName/Desktop/sales-analytics-powerbi

# Or simply:
# Right-click on folder → Git Bash Here
```

---

## 🔧 STEP 4: Initialize Git Repo

```bash
# Initialize Git in folder
git init

# Output: Initialized empty Git repository in...
```

---

## 📝 STEP 5: Add All Files

```bash
# Check status (what's ready for commit)
git status

# Add all files
git add .

# Check again (everything should be green)
git status
```

**What's being added:**
- ✅ README.md
- ✅ Data/SalesData.xlsx
- ✅ Documentation/*.md
- ✅ .gitignore
- ✅ LICENSE
- ✅ CHANGELOG.md

---

## 💾 STEP 6: Create First Commit

```bash
# Commit with message
git commit -m "Initial commit: Sales Analytics Power BI project"

# Output: 
# [main abc1234] Initial commit: Sales Analytics Power BI project
# X files changed, Y insertions(+)
```

---

## 🌐 STEP 7: Create GitHub Repository

### On GitHub.com:

1. **Login to GitHub**
2. Click **+** (top right) → **New repository**
3. **Repository name**: `sales-analytics-powerbi`
4. **Description**: "Power BI Sales Analytics Dashboard with 100+ transactions"
5. **Public** (so it's visible in your portfolio)
6. **DO NOT** check "Add README" (you already have one locally)
7. **DO NOT** check "Add .gitignore" (you already have one)
8. Click **Create repository**

---

## 🔗 STEP 8: Connect Local Repo to GitHub

```bash
# Add remote (copy URL from GitHub)
git remote add origin https://github.com/nikolakotlaja25-web/sales-analytics-powerbi.git

# Verify remote
git remote -v
# Output:
# origin  https://github.com/nikolakotlaja25-web/... (fetch)
# origin  https://github.com/nikolakotlaja25-web/... (push)
```

---

## ⬆️ STEP 9: Push to GitHub

```bash
# Rename branch to main (if needed)
git branch -M main

# Push to GitHub
git push -u origin main
```

### If it asks for authentication:
1. **Username**: your GitHub username
2. **Password**: DO NOT use password, use **Personal Access Token** instead

#### How to get Personal Access Token:
1. GitHub → Settings → Developer settings
2. Personal access tokens → Tokens (classic)
3. Generate new token
4. Scope: ✅ repo (all suboptions)
5. Copy token (SAVE IT!)
6. Paste as "password" in Git Bash

---

## 🎉 STEP 10: Verify on GitHub

1. Go to `https://github.com/nikolakotlaja25-web/sales-analytics-powerbi`
2. You should see:
   - ✅ README.md (displayed automatically)
   - ✅ Folder structure
   - ✅ All files

---

## 📸 STEP 11: Add Screenshots (later)

### After you create the Power BI dashboard:

Take 3 screenshots (one for each page):
- Page 1: Sales Overview → save as `page1_sales_overview.png`
- Page 2: Product Analysis → save as `page2_product_analysis.png`
- Page 3: Customer Insights → save as `page3_customer_insights.png`

Then upload to GitHub:

```bash
# Add all screenshots to Git
git add Screenshots/page1_sales_overview.png
git add Screenshots/page2_product_analysis.png
git add Screenshots/page3_customer_insights.png

# Or add all at once
git add Screenshots/

# Commit
git commit -m "Add all 3 dashboard page screenshots"

# Push
git push
```

---

## 🔄 STEP 12: Future Changes

### Every time you change something:

```bash
# 1. Check what changed
git status

# 2. Add changes
git add .

# 3. Commit with descriptive message
git commit -m "Add YTD sales measure and update documentation"

# 4. Push to GitHub
git push
```

---

## 📚 Additional Git Commands

### View history:
```bash
git log --oneline
```

### Revert file to previous version:
```bash
git checkout -- filename.txt
```

### Create new branch (for experiments):
```bash
git checkout -b feature/new-dashboard
```

### Switch back to main:
```bash
git checkout main
```

### Merge branch:
```bash
git merge feature/new-dashboard
```

---

## 🛠️ Troubleshooting

### Problem: "git: command not found"
**Solution**: Git is not installed or not in PATH. Reinstall Git.

### Problem: "fatal: not a git repository"
**Solution**: You're not in the right folder. `cd` to project and `git init`

### Problem: "Permission denied (publickey)"
**Solution**: Use HTTPS instead of SSH, or setup SSH key

### Problem: "Updates were rejected"
**Solution**: 
```bash
git pull origin main --rebase
git push
```

### Problem: Accidentally added .pbix file (large)
**Solution**:
```bash
# Remove from staging
git reset HEAD Reports/SalesAnalytics.pbix

# Add to .gitignore
echo "*.pbix" >> .gitignore

# Commit .gitignore
git add .gitignore
git commit -m "Update .gitignore"
```

---

## 🎓 Git Best Practices

### ✅ GOOD:
```bash
git commit -m "Add profit margin calculation to DAX measures"
git commit -m "Fix date filter bug in Sales Overview page"
git commit -m "Update README with installation instructions"
```

### ❌ BAD:
```bash
git commit -m "update"
git commit -m "fix"
git commit -m "asdfasdf"
```

### Commit frequently:
- 👍 Small, focused changes
- 👍 Clear commit messages
- 👍 Commit after each feature/bug fix

### DO NOT commit:
- ❌ .pbix temporary files
- ❌ Excel ~$ temporary files
- ❌ Personal information (API keys, passwords)
- ❌ Huge binary files (>100MB)

---

## 🏆 GitHub Portfolio Tips

### README.md highlighting:
- Add **badges** (shields.io)
- Add **screenshot** of dashboard
- List **technologies** used
- Link to **live demo** (if available)

### Pin repository:
1. GitHub profile → Customize your pins
2. Select this project
3. It will appear at the top of your profile

### Add topics:
1. Repo → About (gear icon)
2. Topics: `power-bi`, `dax`, `data-analytics`, `dashboard`, `excel`

### Share on LinkedIn:
- Post project on LinkedIn
- Add link to GitHub repo
- Add dashboard screenshot

---

## 🔐 .pbix File Handling

### Option 1: DO NOT upload .pbix to GitHub
```bash
# Add to .gitignore
echo "*.pbix" >> .gitignore
```
**Reason**: .pbix files are large and binary (hard to track changes)

### Option 2: Upload .pbix (if you want others to open it)
```bash
# Git LFS (Large File Storage)
git lfs install
git lfs track "*.pbix"
git add .gitattributes
git commit -m "Configure Git LFS for .pbix files"
```

**Note**: GitHub has a limit of 100MB per file (50MB recommended)

---

## ✅ Final Checklist

Before pushing to GitHub, check:

- [ ] README.md is complete and clear
- [ ] .gitignore includes temp files
- [ ] No sensitive data (passwords, keys)
- [ ] Folder structure is logical
- [ ] Documentation is updated
- [ ] Screenshot is added (or placeholder)
- [ ] LICENSE file exists
- [ ] Commit messages are clear

---

**🎉 Done! Your Power BI project is now on GitHub! 🎉**

Share link:
```
https://github.com/nikolakotlaja25-web/sales-analytics-powerbi
```

Add it to:
- ✅ LinkedIn (Featured section)
- ✅ CV/Resume
- ✅ Portfolio website
- ✅ GitHub pinned repositories

---

## 📞 Help

Questions? Issues? Bug reports?
- Open [GitHub Issue](https://github.com/nikolakotlaja25-web/sales-analytics-powerbi/issues)
- Ask on [Stack Overflow](https://stackoverflow.com/questions/tagged/power-bi)
- Community: [Power BI Community Forums](https://community.powerbi.com/)
