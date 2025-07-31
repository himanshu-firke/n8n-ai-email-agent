# 🛠️ Setup Guide - AI Email Agent

This guide will walk you through setting up the AI Email Agent workflow step by step.

## 📋 Prerequisites Checklist

- [ ] n8n instance running (version 1.0+)
- [ ] Google Cloud Console account
- [ ] Gmail account
- [ ] Google Sheets document created
- [ ] Google AI Studio account (for Gemini API)

## 🔧 Step-by-Step Setup

### Step 1: Google Cloud Console Setup

1. **Create a New Project**
   - Go to [Google Cloud Console](https://console.cloud.google.com/)
   - Click "New Project"
   - Name it "n8n-email-agent"

2. **Enable Required APIs**
   - Gmail API
   - Google Sheets API
   - Google Drive API (for Sheets access)

3. **Create OAuth2 Credentials**
   - Go to "Credentials" → "Create Credentials" → "OAuth 2.0 Client IDs"
   - Application type: "Web application"
   - Add authorized redirect URIs:
     - `http://localhost:5678/rest/oauth2-credential/callback`
     - `https://your-n8n-instance.com/rest/oauth2-credential/callback`

### Step 2: Google AI Studio Setup

1. **Get Gemini API Key**
   - Visit [Google AI Studio](https://ai.google.dev/)
   - Click "Get API Key"
   - Create a new API key
   - Copy and save the key securely

### Step 3: Google Sheets Preparation

1. **Create Your Spreadsheet**
   - Open [Google Sheets](https://sheets.google.com)
   - Create a new spreadsheet
   - Name it "Email Agent Data"

2. **Set Up Columns**
   - Column A: "Name"
   - Column B: "Email"
   - Column C: "Score"

3. **Get Sheet Information**
   - Copy the spreadsheet ID from the URL
   - Note the sheet name (usually "Sheet1")

### Step 4: n8n Credential Configuration

#### Gmail OAuth2 Credential

1. In n8n, go to **Settings** → **Credentials**
2. Click **Add Credential**
3. Select **Gmail OAuth2 API**
4. Fill in:
   - **Client ID**: From Google Cloud Console
   - **Client Secret**: From Google Cloud Console
   - **Scope**: `https://www.googleapis.com/auth/gmail.modify`
5. Click **Connect my account**
6. Complete OAuth flow
7. Test the connection

#### Google Sheets OAuth2 Credential

1. Click **Add Credential**
2. Select **Google Sheets OAuth2 API**
3. Fill in:
   - **Client ID**: Same as Gmail
   - **Client Secret**: Same as Gmail
   - **Scope**: `https://www.googleapis.com/auth/spreadsheets`
4. Complete OAuth flow
5. Test access to your spreadsheet

#### Google Gemini API Credential

1. Click **Add Credential**
2. Select **Google PaLM API**
3. Fill in:
   - **API Key**: From Google AI Studio
4. Test the connection

### Step 5: Import and Configure Workflow

1. **Import Workflow**
   - Download `email-agent-workflow.json`
   - In n8n: **Import from File**
   - Select the JSON file

2. **Update Node Configurations**

   **Google Sheets Nodes:**
   - Replace document ID with your spreadsheet ID
   - Update sheet name if different
   - Verify column mapping

   **Gmail Nodes:**
   - Assign your Gmail OAuth2 credential
   - Test send/receive functionality

   **Gemini AI Node:**
   - Assign your Google PaLM API credential
   - Verify model name: `models/gemini-2.5-pro`

3. **Test Individual Nodes**
   - Execute each node manually
   - Verify credentials work
   - Check data flow

### Step 6: Activate and Test

1. **Activate Workflow**
   - Toggle the workflow to "Active"
   - Note the webhook URL from chat trigger

2. **Test Chat Interface**
   - Use the webhook URL to send test messages
   - Try basic commands:
     - "Hello, can you help me?"
     - "Send a test email to myself"
     - "Add a test row to the sheet"

## 🔍 Verification Steps

### Test Email Functionality
```
Send an email to your-email@example.com with subject "Test" and message "This is a test email from n8n"
```

### Test Sheets Functionality
```
Add a new row with Name: "Test User", Email: "test@example.com", Score: "100"
```

### Test Retrieval
```
Get my latest 5 emails
```

## 🚨 Troubleshooting

### Common Issues and Solutions

**OAuth2 Authentication Failed**
- Check redirect URIs in Google Cloud Console
- Verify client ID and secret
- Ensure APIs are enabled

**Gemini API Errors**
- Verify API key is correct
- Check quota limits
- Ensure model name is exact: `models/gemini-2.5-pro`

**Sheets Access Denied**
- Verify spreadsheet ID is correct
- Check OAuth2 scopes include spreadsheets
- Ensure sheet name matches exactly

**Webhook Not Responding**
- Check n8n instance is accessible
- Verify webhook URL is correct
- Test with manual execution first

## 📊 Monitoring and Logs

1. **Execution History**
   - Monitor workflow executions in n8n
   - Check for errors and success rates

2. **API Usage**
   - Monitor Google Cloud Console for API usage
   - Watch Gemini API quotas

3. **Performance**
   - Track response times
   - Monitor memory usage in AI agent

## 🔒 Security Best Practices

1. **API Keys**
   - Store securely in n8n credentials
   - Never commit to version control
   - Rotate regularly

2. **OAuth2 Tokens**
   - Monitor token expiration
   - Set up refresh mechanisms
   - Limit scopes to minimum required

3. **Webhook Security**
   - Use HTTPS in production
   - Consider webhook authentication
   - Monitor for unauthorized access

## 📈 Optimization Tips

1. **Memory Management**
   - Adjust memory buffer window size
   - Clear old conversations periodically

2. **API Efficiency**
   - Batch operations when possible
   - Implement rate limiting
   - Cache frequently used data

3. **Error Handling**
   - Add retry logic for failed operations
   - Implement fallback mechanisms
   - Log errors for debugging

---

✅ **Setup Complete!** Your AI Email Agent is now ready to use.
