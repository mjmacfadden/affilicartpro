# AffiliCart Light - Email Capture Setup Guide

This guide walks you through setting up Google Sheets + Apps Script to capture emails for the AffiliCart Light free download.

## Step 1: Create a Google Sheet

1. Go to [Google Sheets](https://sheets.google.com)
2. Click "New" and create a blank spreadsheet
3. Name it: "AffiliCart Light Emails"
4. Create a header row with: `Email` | `Timestamp`
5. Note down your **Sheet ID** from the URL:
   - URL looks like: `https://docs.google.com/spreadsheets/d/{SHEET_ID}/edit`
   - Copy the SHEET_ID value (long string of characters between `/d/` and `/edit`)

## Step 2: Create Google Apps Script

1. Go to [Google Apps Script](https://script.google.com)
2. Click "New Project" (top left)
3. Name it: "AffiliCart Email Capture"
4. Delete any default code
5. Paste this code:

```javascript
const SHEET_ID = "YOUR_SHEET_ID_HERE"; // Replace with your Sheet ID
const SHEET_NAME = "Sheet1"; // Default sheet name (change if different)

function doPost(e) {
  try {
    const email = e.parameter.email;
    
    // Validate email
    if (!email || !isValidEmail(email)) {
      return ContentService.createTextOutput(
        JSON.stringify({ success: false, error: "Invalid email address" })
      ).setMimeType(ContentService.MimeType.JSON);
    }
    
    // Get the sheet
    const sheet = SpreadsheetApp.openById(SHEET_ID).getSheetByName(SHEET_NAME);
    
    // Add header row if empty
    if (sheet.getLastRow() === 0) {
      sheet.appendRow(["Email", "Timestamp"]);
    }
    
    // Check for duplicate
    const data = sheet.getDataRange().getValues();
    for (let i = 1; i < data.length; i++) {
      if (data[i][0] === email) {
        return ContentService.createTextOutput(
          JSON.stringify({ success: false, error: "Email already registered" })
        ).setMimeType(ContentService.MimeType.JSON);
      }
    }
    
    // Add the email
    sheet.appendRow([email, new Date()]);
    
    return ContentService.createTextOutput(
      JSON.stringify({ success: true, message: "Email captured successfully" })
    ).setMimeType(ContentService.MimeType.JSON);
  } catch (error) {
    return ContentService.createTextOutput(
      JSON.stringify({ success: false, error: error.toString() })
    ).setMimeType(ContentService.MimeType.JSON);
  }
}

function isValidEmail(email) {
  const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
  return emailRegex.test(email);
}
```

6. Replace `"YOUR_SHEET_ID_HERE"` with your Sheet ID from Step 1
7. Save the script (Ctrl+S or Cmd+S)

## Step 3: Deploy as Web App

1. Click "Deploy" (top right)
2. Click "New deployment" (top right of the modal)
3. Select "Select type" dropdown → choose **"Web app"**
4. Fill in:
   - Execute as: [Your Google Account]
   - Who has access: **"Anyone"** (important!)
5. Click "Deploy"
6. A popup will appear with your **deployment URL**
7. Copy the entire URL (looks like: `https://script.googleapis.com/macros/s/{SCRIPT_ID}/userweb`)

## Step 4: Add the Deployment URL to index.html

1. Open `/index.html`
2. Find this line (around line 400+):
   ```javascript
   const GOOGLE_SCRIPT_URL = 'YOUR_GOOGLE_SCRIPT_URL_HERE';
   ```
3. Replace with your deployment URL:
   ```javascript
   const GOOGLE_SCRIPT_URL = 'https://script.googleapis.com/macros/s/YOUR_SCRIPT_ID/userweb';
   ```
4. Save the file

## Step 5: Test It Out

1. Open your site locally or deployed
2. Click the "Download Free" button
3. Enter a test email
4. Click "Get Download Link"
5. You should see:
   - A spinner briefly
   - Success message
   - Download link appears
6. Check your Google Sheet - the email should be there!

## Troubleshooting

**"Something went wrong" error:**
- Check that SHEET_ID is correct
- Check that SHEET_NAME matches your sheet (default is "Sheet1")
- Make sure the deployment has "Anyone" access

**Email not appearing in sheet:**
- Verify the deployment URL is correct
- Check that the Apps Script is deployed as "Web app"
- Make sure "Execute as" is set to your account

**Duplicate email handling:**
- The script already prevents duplicate emails
- Users will see "Email already registered" message

## Future Enhancements

You could add:
- Send a welcome email with download link (Gmail API)
- Add email confirmation before showing download
- Track download metrics
- Send onboarding emails via Mailchimp/ConvertKit

Let me know if you need help with any of these steps!
