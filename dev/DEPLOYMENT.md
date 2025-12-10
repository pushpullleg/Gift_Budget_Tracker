# Deployment Guide

Complete guide for deploying the Gift Budget Tracker to GitHub Pages.

## Quick Checklist

- [ ] Google Sheet created with "Transactions" tab
- [ ] Google Apps Script deployed as Web App
- [ ] GitHub repository created (Public)
- [ ] Files pushed to GitHub
- [ ] GitHub Pages enabled
- [ ] Test the live site

---

## Step 1: Create GitHub Repository

1. Go to: https://github.com/new
2. **Repository name**: `gift-budget-tracker` (or any name)
3. **Visibility**: **Public** (required for free GitHub Pages)
4. **DO NOT** check "Initialize with README"
5. Click **"Create repository"**
6. **Copy the repository URL** (e.g., `https://github.com/YOUR_USERNAME/gift-budget-tracker.git`)

---

## Step 2: Push Files to GitHub

### Option A: Git Command Line (Recommended)

Open **PowerShell** in your project folder:

```powershell
# Navigate to project folder
cd "C:\Users\50380788\Documents\Sheet_for_Wife"

# Initialize Git (if not already done)
git init

# Add files
git add index.html css/style.css js/script.js README.md docs/ backend/Code.gs.example

# Commit
git commit -m "Initial commit - Gift Budget Tracker"

# Rename branch to main (if needed)
git branch -M main

# Add remote (replace YOUR_USERNAME and REPO_NAME)
git remote add origin https://github.com/YOUR_USERNAME/gift-budget-tracker.git

# Push
git push -u origin main
```

### Option B: GitHub Desktop

1. Download [GitHub Desktop](https://desktop.github.com/)
2. File → Clone Repository → Choose your new repo
3. Copy files into the cloned folder
4. Commit and push

### Option C: Drag & Drop (One-time only)

1. On GitHub repo page, click "uploading an existing file"
2. Drag and drop: `index.html`, `css/style.css`, `js/script.js`, `README.md`
3. Click "Commit changes"

---

## Step 3: Enable GitHub Pages

1. Go to your repository on GitHub
2. Click **"Settings"** tab
3. Click **"Pages"** in left sidebar
4. Under **"Source"**, select **"Deploy from a branch"**
5. Choose:
   - **Branch**: `main`
   - **Folder**: `/ (root)`
6. Click **"Save"**

---

## Step 4: Wait & Access

1. Wait 1-2 minutes for GitHub to build your site
2. Your site will be live at:
   - `https://YOUR_USERNAME.github.io/gift-budget-tracker/`
3. You'll see the URL in the Pages settings after it's ready

---

## Files to Deploy

✅ **These files should be in git:**
- `index.html`
- `css/style.css`
- `js/script.js`
- `README.md`
- `docs/` folder
- `backend/Code.gs.example`
- `.gitignore`

❌ **These files are gitignored (not deployed):**
- `backend/Code.gs` (contains sensitive data)
- `dev/` folder (development notes)

---

## Authentication Issues

If Git asks for username/password:

1. **Use a Personal Access Token** instead of password:
   - Go to: https://github.com/settings/tokens
   - Click "Generate new token (classic)"
   - Select scope: `repo` (full control)
   - Copy the token and use it as your password

2. Or use **GitHub Desktop** (easier for beginners)

---

## Verify Deployment

1. Open your GitHub Pages URL
2. The budget should load automatically
3. Try adding a test expense
4. Check your Google Sheet - the entry should appear!

---

## Troubleshooting

**Site not loading?**
- Wait 2-3 minutes (first deployment takes time)
- Check Settings → Pages for any errors
- Make sure repository is Public

**Still getting network errors?**
- See `TROUBLESHOOTING.md` for detailed debugging
- Verify API key is in both Code.gs and js/script.js
- Check browser console (F12) for specific errors

---

## Updating After Changes

```powershell
# After making changes to files
git add .
git commit -m "Description of changes"
git push
```

GitHub Pages will automatically rebuild (takes 1-2 minutes).

