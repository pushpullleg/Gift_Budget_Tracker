# Budget Tracker - Simple Expense Entry Web App

A simple, mobile-friendly web application for tracking expenses. Hosted on GitHub Pages, connects to Google Sheets via Google Apps Script.

## Features

- **Ultra-simple form**: Just amount, category, and optional notes
- **Mobile-first design**: Large touch-friendly buttons, optimized for phone use
- **Quick entry buttons**: $5, $10, $20, $50 for common purchases
- **Undo functionality**: Remove the last entry with one click
- **Real-time validation**: Prevents errors before submission
- **Auto-timestamping**: Date added automatically
- **Dynamic budget tracking**: Budget remaining updates automatically from Google Sheets

## Setup Instructions

### Step 1: Create Google Sheet

1. Go to [Google Sheets](https://sheets.google.com) and create a new spreadsheet
2. Rename the first tab to `Transactions` (or keep it as is if it's already named)
3. In row 1, add these headers: `Date`, `Amount`, `Category`, `Notes`
4. (Optional) Add summary rows at the top:
   - Row 1: Headers
   - Row 2: `Starting Budget: $2500` (or your amount)
   - Row 3: `Total Spent: =SUM(B4:B)` (adjust row number based on where data starts)
   - Row 4: `Remaining: =B2-B3`
   - Row 5: Empty row
   - Row 6: Headers (`Date`, `Amount`, `Category`, `Notes`)
   - Data starts from row 7

5. Copy the **Spreadsheet ID** from the URL:
   - URL format: `https://docs.google.com/spreadsheets/d/SPREADSHEET_ID/edit`
   - Copy the part between `/d/` and `/edit`

### Step 2: Set Up Google Apps Script

1. Go to [Google Apps Script](https://script.google.com)
2. Click "New Project"
3. Delete the default `myFunction` code
4. Copy the entire contents of `Code.gs` from this repository
5. Paste it into the Apps Script editor
6. Update the configuration at the top of `Code.gs`:
   - Replace `YOUR_SPREADSHEET_ID_HERE` with your actual Spreadsheet ID
   - Replace `YOUR_API_KEY_HERE` with a secure random string
     - Generate one at: https://www.random.org/strings/
     - Use: 32 characters, alphanumeric
     - Example: `a7f3k9m2p5q8r1t4v6w0x2y5z8b1c3`
   - Update `STARTING_BUDGET` with your budget amount (default: 2500)
7. Save the project (Ctrl+S or Cmd+S)
8. Click "Deploy" → "New deployment"
9. Click the gear icon ⚙️ next to "Select type" → Choose "Web app"
10. Configure:
    - **Description**: "Budget Tracker API" (or any name)
    - **Execute as**: Me
    - **Who has access**: Anyone
11. Click "Deploy"
12. **Copy the Web App URL** - you'll need this for the next step
13. Click "Authorize access" and grant permissions to your Google account

### Step 3: Configure the Web App

1. Open `script.js` in this repository
2. Update the configuration at the top:
   - Replace `YOUR_APPS_SCRIPT_URL_HERE` with the Web App URL from Step 2
   - Replace `YOUR_API_KEY_HERE` with the same API key you used in `Code.gs`
3. Save the file

### Step 4: Deploy to GitHub Pages

#### Option A: New Repository

1. Create a new repository on GitHub (e.g., `budget-tracker`)
2. Clone it to your computer:
   ```bash
   git clone https://github.com/YOUR_USERNAME/budget-tracker.git
   cd budget-tracker
   ```
3. Copy all files from this repository to the cloned folder:
   - `index.html`
   - `style.css`
   - `script.js`
   - `README.md`
4. Commit and push:
   ```bash
   git add .
   git commit -m "Initial commit - Budget Tracker"
   git push origin main
   ```
5. Go to your repository on GitHub
6. Click "Settings" → "Pages"
7. Under "Source", select "Deploy from a branch"
8. Choose `main` branch and `/ (root)` folder
9. Click "Save"
10. Your app will be available at: `https://YOUR_USERNAME.github.io/budget-tracker/`

#### Option B: Existing Repository

1. Add the files to your existing repository
2. Follow steps 5-10 from Option A

### Step 5: Test the App

1. Open your GitHub Pages URL on your phone
2. Try adding a test expense:
   - Enter an amount (e.g., `10.00`)
   - Select a category
   - Click "Add Expense"
3. Check your Google Sheet - the entry should appear
4. Test the "Undo Last Entry" button

## Usage

1. **Bookmark the page** on your phone for easy access
2. **Add expenses**:
   - Enter amount (or use quick buttons)
   - Select category
   - Optionally add notes
   - Click "Add Expense"
3. **Undo mistakes**: Click "Undo Last Entry" if you made an error
4. **View data**: Check your Google Sheet anytime to see all expenses

## Categories

- Groceries
- Dining
- Shopping
- Travel
- Health
- Personal
- Gifts
- Misc

## Troubleshooting

### "Please configure API_URL and API_KEY"
- Make sure you updated the `CONFIG` object in `script.js`

### "Invalid API key"
- Ensure the API key in `script.js` matches the one in `Code.gs`
- Check for extra spaces or typos

### "Failed to add expense"
- Verify your Google Apps Script is deployed correctly
- Check that the Spreadsheet ID is correct
- Ensure the sheet tab is named "Transactions"
- Check Apps Script execution logs: Apps Script → Executions

### Data not appearing in sheet
- Check that you granted permissions to Apps Script
- Verify the Spreadsheet ID is correct
- Check Apps Script logs for errors

### CORS errors in browser console
- Make sure Apps Script is deployed as "Web app" (not API)
- Verify "Who has access" is set to "Anyone"

## Security Notes

- The API key is visible in the frontend code (this is acceptable for personal use)
- The web app URL is publicly accessible but protected by API key validation
- For higher security, consider using environment variables or a build process
- Never commit sensitive data to public repositories

## Customization

### Change Starting Budget
- Edit the summary row in your Google Sheet (row 2 in the example)

### Add More Categories
1. Update `Code.gs`: Add to `allowedCategories` array
2. Update `index.html`: Add new category button in the grid
3. Update `style.css`: Adjust grid if needed (currently 2 columns)

### Change Date Format
- Currently uses ISO format (YYYY-MM-DD)
- To change, modify the date formatting in `Code.gs` → `doPost()` function

## Support

If you encounter issues:
1. Check the browser console for errors (F12 → Console)
2. Check Google Apps Script execution logs
3. Verify all configuration values are correct
4. Ensure all permissions are granted

## License

Free to use for personal projects.

