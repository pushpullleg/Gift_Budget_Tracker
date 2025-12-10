# Troubleshooting Guide

Common issues and solutions for the Gift Budget Tracker.

---

## Network Error / CORS Issues

### Step 1: Check Browser Console

1. Open your live site
2. Press **F12** (or right-click → Inspect)
3. Click **"Console"** tab
4. Try adding an expense
5. **Look for the exact error message**

Common errors:
- `CORS policy` → Deployment issue
- `Invalid API key` → API key mismatch
- `Failed to fetch` → Network/CORS issue
- `404 Not Found` → Wrong URL

### Step 2: Verify Google Apps Script Setup

**Check API Key in Code.gs:**
1. Go to [Google Apps Script](https://script.google.com)
2. Open your project
3. Check the `API_KEY` in CONFIG - should match `js/script.js`
4. If wrong, fix it and **SAVE** (Ctrl+S)

**Verify Deployment:**
1. In Google Apps Script, click **"Deploy"** → **"Manage deployments"**
2. Make sure there's a deployment with:
   - **Type**: Web app
   - **Execute as**: Me
   - **Who has access**: Anyone (CRITICAL for CORS)
3. If not, create a new deployment:
   - Click **"New deployment"**
   - Gear icon → **"Web app"**
   - Execute as: **Me**
   - Who has access: **Anyone**
   - Click **"Deploy"**

**Check Execution Logs:**
1. In Google Apps Script, click **"Executions"** (left sidebar)
2. Try adding an expense from your live site
3. Check if there are any execution logs
4. If you see errors, click on them to see details

### Step 3: Test the Google Apps Script URL

Try accessing your Google Apps Script URL directly:
```
https://script.google.com/macros/s/YOUR_SCRIPT_ID/exec
```

**Expected**: You should see "Script function not found: doGet" (this is normal - it means the script is deployed)

**If you see**: "Script not found" or "404" → The deployment is wrong

---

## Common Fixes

### Fix 1: Redeploy Google Apps Script

Sometimes you need to create a NEW deployment:

1. In Google Apps Script, click **"Deploy"** → **"Manage deployments"**
2. Click the **pencil icon** (edit) on your deployment
3. Click **"New version"**
4. Click **"Deploy"**
5. **Copy the new URL** (it might be the same or different)
6. Update `js/script.js` if the URL changed
7. Commit and push to GitHub

### Fix 2: Check Spreadsheet ID

1. In Google Apps Script, check the `SPREADSHEET_ID` in CONFIG
2. Make sure it has your actual Spreadsheet ID (not the placeholder)
3. Get it from your Google Sheet URL: `docs.google.com/spreadsheets/d/SPREADSHEET_ID/edit`

### Fix 3: Verify Sheet Name

1. Make sure your Google Sheet has a tab named exactly **"Transactions"** (case-sensitive)
2. Make sure row 1 has headers: `Date`, `Amount`, `Category`, `Notes`

### Fix 4: API Key Mismatch

**Most common issue!**

1. Check `backend/Code.gs` - API_KEY value
2. Check `js/script.js` - API_KEY value
3. They must be **exactly the same** (including quotes, no spaces)
4. If different, update both and redeploy

---

## Testing Locally

### The Problem

When you open `index.html` directly in Chrome (double-click), it uses the `file://` protocol. Browsers block cross-origin requests from `file://` for security reasons, which causes "network error."

### Solution: Use a Local Server

**Option A: Python**
```bash
python -m http.server 8000
# Then open: http://localhost:8000
```

**Option B: Node.js**
```bash
npx http-server
# Then open the URL shown
```

**Option C: VS Code Live Server**
1. Install "Live Server" extension
2. Right-click `index.html` → "Open with Live Server"

### Or Just Deploy

**The CORS issue only happens with `file://` protocol.** Once deployed to GitHub Pages (or any web server), it will work perfectly. You can test directly on GitHub Pages without local setup.

---

## Testing API Directly (Advanced)

**Using curl:**
```bash
curl -X POST "YOUR_SCRIPT_URL" \
  -H "Content-Type: text/plain;charset=utf-8" \
  -d '{"apiKey":"YOUR_API_KEY","action":"getBudget"}'
```

This should return JSON with budget info if everything is working.

---

## Quick Checklist

- [ ] API key in Code.gs matches js/script.js exactly
- [ ] Spreadsheet ID is set in Code.gs (not placeholder)
- [ ] Google Apps Script is deployed as "Web app"
- [ ] "Who has access" is set to "Anyone" (CRITICAL)
- [ ] Sheet tab is named "Transactions" (case-sensitive)
- [ ] Sheet has headers: Date, Amount, Category, Notes
- [ ] Browser console shows specific error (check F12)
- [ ] GitHub Pages repository is Public

---

## Most Likely Issues (in order)

1. **API key not set in Code.gs** (90% of issues)
2. **Deployment not set to "Anyone"** (CORS issue)
3. **Spreadsheet ID wrong** in Code.gs
4. **Sheet tab name wrong** (should be "Transactions")
5. **Testing locally with file://** (use local server or deploy)
