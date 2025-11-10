# Quick Setup (30 minutes)

## Prerequisites
- [x] n8n instance (cloud or self-hosted)
- [x] Google account with access to Google Forms and Google Apps Script
- [x] Airtable account with a base and table ready
- [x] Slack workspace with permissions to add integrations
- [ ] Airtable API Key and Base ID ready
- [ ] Slack Webhook URL ready

## Steps

### 1. Prepare Airtable
1. Create a new Airtable Base or use an existing one.
2. Create a new Table (e.g., "Leads") with columns matching your Google Form fields (e.g., "Name", "Email", "Message").
3. Obtain your Airtable API Key (Account settings) and Base ID (Airtable API documentation for your base).

### 2. Prepare Slack
1. In your Slack workspace, go to "Integrations" or "Apps".
2. Search for "Incoming WebHooks" and add it to your workspace.
3. Choose a channel for notifications and copy the generated Webhook URL.

### 3. Configure Google Form Webhook (via Google Apps Script)
1. Open your Google Form.
2. Go to "Responses" tab, then click the three vertical dots and select "Get add-ons".
3. Search for and install "Form Publisher" or a similar add-on that allows custom webhooks, or use Google Apps Script directly:
   - Go to "Extensions" -> "Apps Script".
   - Replace the existing code with a script that sends form submission data to your n8n webhook.
   - Example Google Apps Script (replace `YOUR_N8N_WEBHOOK_URL` with your n8n webhook URL):
     ```javascript
     function onSubmit(e) {
       var form = e.source;
       var response = e.response;
       var items = response.getItemResponses();
       var payload = {};

       for (var i = 0; i < items.length; i++) {
         var item = items[i];
         payload[item.getItem().getTitle()] = item.getResponse();
       }

       var options = {
         'method' : 'post',
         'contentType': 'application/json',
         'payload' : JSON.stringify(payload)
       };

       UrlFetchApp.fetch('YOUR_N8N_WEBHOOK_URL', options);
     }

     function createFormTrigger() {
       var form = FormApp.getActiveForm();
       ScriptApp.newTrigger('onSubmit')
           .forForm(form)
           .onFormSubmit()
           .create();
     }
     ```
   - Save the script and run `createFormTrigger` once to set up the trigger.

### 4. Import Workflow
```bash
# Copy workflow.json content → n8n UI → Import from JSON
```

### 5. Configure Credentials
1. In n8n: Credentials → New → Airtable API.
2. Add required credentials:
   - **API Key**: Paste your Airtable API Key.
3. In n8n: Credentials → New → Slack API.
4. Add required credentials:
   - **Webhook URL**: Paste your Slack Webhook URL.

*Note: workflow.json has redacted credentials for security*

### 6. Update Node References
After import, re-select:
- **Airtable (Add Record)**: Select your Airtable credential, Base ID, and Table Name. Map the Google Form fields to your Airtable columns.
- **Slack (Send Message)**: Select your Slack credential and customize the message content using expressions like `{{ $json.Name }}`.

### 7. Test & Activate
```bash
# Test execution first by submitting a test form entry
# Check executions tab for errors
# Toggle "Active" when confirmed working
```

## Troubleshooting

**Problem 1: Google Form submissions are not triggering the n8n workflow.**
- Symptom: No executions appear in n8n after submitting the Google Form.
- Solution: Verify that the Google Apps Script is correctly set up with the n8n webhook URL and that the `onSubmit` trigger is active. Check the Apps Script execution logs for errors.

**Problem 2: Data is not being added to Airtable.**
- Symptom: n8n workflow runs, but no new records appear in Airtable.
- Solution: Ensure the Airtable credential, Base ID, and Table Name are correctly configured in the "Airtable (Add Record)" node. Verify that the field mappings between the Google Form data and Airtable columns are correct.

**Problem 3: Slack messages are not being sent.**
- Symptom: n8n workflow runs, but no Slack notifications are received.
- Solution: Check that the Slack Webhook URL is correctly configured in the Slack credential and selected in the "Slack (Send Message)" node. Ensure the Slack app has permission to post to the selected channel.

## Advanced Configuration (Optional)

- **Conditional Logic**: Add conditional nodes to process form submissions differently based on their content (e.g., route high-priority leads to a different Slack channel).
- **Data Validation**: Implement data validation within n8n to ensure form submissions meet specific criteria before being processed.
- **Error Notifications**: Configure additional nodes to send error notifications to an admin if the workflow fails at any step.

