# Reference Notes

Quick reference for one-time tasks and project information.

---

## Project Renaming

If you need to rename the project:

1. **Rename local folder:**
   ```powershell
   cd "C:\Users\50380788\Documents"
   Rename-Item -Path "Sheet_for_Wife" -NewName "gift-budget-tracker"
   ```

2. **Rename GitHub repository:**
   - Go to repository Settings
   - Change repository name
   - Update git remote: `git remote set-url origin NEW_URL`

3. **Update URLs:**
   - Old: `https://pushpullleg.github.io/Sheet_for_Wife/`
   - New: `https://pushpullleg.github.io/gift-budget-tracker/`

---

## Current Configuration

**API Key:** `43619930614212440190980972744666`  
**Google Apps Script URL:** `https://script.google.com/macros/s/AKfycbyNel64mjqFn1PeAQYXzUT6_JIhUNqPGk2GQEP69hDpOyMZjh8VUjNgxQiYJdDaIdE3tw/exec`  
**GitHub Pages URL:** `https://pushpullleg.github.io/Sheet_for_Wife/`

**Note:** These are in production. For security, rotate if exposed.

---

## Project Structure

```
gift-budget-tracker/
├── index.html              # Main app
├── css/style.css           # Styles
├── js/script.js           # Frontend logic
├── docs/                   # User docs
├── backend/Code.gs        # Google Apps Script (gitignored)
└── dev/                    # This folder (dev notes)
```

---

## Key Commands

**Git:**
```powershell
git add .
git commit -m "Message"
git push
```

**Local Server:**
```bash
python -m http.server 8000
```

---

## Important Notes

- `backend/Code.gs` is gitignored (contains sensitive data)
- `js/script.js` is currently in git (for deployment)
- Always test on GitHub Pages, not locally with file://
- API key must match in both Code.gs and js/script.js

