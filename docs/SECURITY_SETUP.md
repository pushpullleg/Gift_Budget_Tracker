# Security Setup - Using Script Properties

This guide explains how to use Google Apps Script's **Script Properties** (equivalent to environment variables) to securely store sensitive configuration values.

## Why Use Script Properties?

- **Security**: Values are stored separately from your code
- **Not visible in code editor**: Properties are hidden by default
- **Easy to update**: Change values without editing code
- **Best practice**: Recommended by Google for sensitive data

## Setup Instructions

### Step 1: Update the setupConfig() Function

1. Open your `Code.gs` in Google Apps Script
2. Find the `setupConfig()` function
3. Replace the placeholder values with your actual values:

```javascript
function setupConfig() {
  const properties = PropertiesService.getScriptProperties();
  
  properties.setProperties({
    'SPREADSHEET_ID': '1Q71J9F-cI5oxZ6SKZrKg-2p5-81W7nHi-cVzk6AeLzo',  // Your actual Sheet ID
    'API_KEY': '43619930614212440190980972744666',                      // Your actual API key
    'SHEET_NAME': 'Transactions',
    'STARTING_BUDGET': '2500'
  });
  
  Logger.log('Configuration saved successfully!');
}
```

### Step 2: Run setupConfig() Once

1. In Google Apps Script editor, select `setupConfig` from the function dropdown
2. Click the **Run** button (▶️)
3. Authorize the script if prompted
4. Check the **Execution log** (View → Logs) - you should see "Configuration saved successfully!"

### Step 3: Verify Values Are Stored

1. In Google Apps Script, go to **Project Settings** (gear icon ⚙️)
2. Scroll down to **Script Properties**
3. You should see your values listed (they're stored securely)

### Step 4: Delete or Comment Out setupConfig()

**IMPORTANT**: After setup, delete or comment out the `setupConfig()` function to prevent accidental overwrites:

```javascript
// function setupConfig() {
//   ... (commented out)
// }
```

Or simply delete the entire function.

## Updating Values Later

If you need to change values later:

### Option A: Use setupConfig() Again

1. Uncomment or recreate `setupConfig()` function
2. Update the values
3. Run it once
4. Delete/comment it out again

### Option B: Use PropertiesService Directly

1. In Google Apps Script, go to **Project Settings** (gear icon ⚙️)
2. Scroll to **Script Properties**
3. Click **Add script property** or edit existing ones
4. Set key-value pairs manually

### Option C: Use a Helper Function

Add this function temporarily:

```javascript
function updateProperty(key, value) {
  PropertiesService.getScriptProperties().setProperty(key, value);
  Logger.log(`Updated ${key}`);
}

// Usage: Run updateProperty('API_KEY', 'new_key_here')
```

## Viewing Current Values

To see what values are currently stored:

```javascript
function viewConfig() {
  const config = getConfig();
  Logger.log('Current configuration:');
  Logger.log('SPREADSHEET_ID: ' + config.SPREADSHEET_ID);
  Logger.log('API_KEY: ' + config.API_KEY);
  Logger.log('SHEET_NAME: ' + config.SHEET_NAME);
  Logger.log('STARTING_BUDGET: ' + config.STARTING_BUDGET);
}
```

Run this function and check the Execution log (View → Logs).

## Security Benefits

✅ **Values not in code**: Can't accidentally commit secrets to git  
✅ **Hidden by default**: Not visible when viewing code  
✅ **Separate storage**: Stored in Google's secure properties system  
✅ **Easy rotation**: Update values without code changes  

## Important Notes

- **Script Properties are per-project**: Each Apps Script project has its own properties
- **Not encrypted at rest**: Google stores them securely, but they're accessible to anyone with script edit access
- **For personal projects**: This is sufficient. For production apps, consider additional security measures
- **Backup**: If you delete the script, properties are lost. Keep a backup of your values

## Troubleshooting

**"Property not found" errors:**
- Make sure you ran `setupConfig()` at least once
- Check Project Settings → Script Properties to verify values exist

**Values not updating:**
- Properties are cached. Try refreshing or redeploying
- Make sure you're updating the correct script project

**Can't see properties:**
- Go to Project Settings (gear icon) → Script Properties
- They're only visible there, not in the code editor

