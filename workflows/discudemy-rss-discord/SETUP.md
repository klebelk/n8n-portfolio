# Quick Setup (15 minutes)

## Prerequisites
- [x] n8n instance (cloud or self-hosted)
- [x] Discord account with permissions to create a bot and manage a server
- [ ] Discord Bot Client ID & Secret ready

## Steps

### 1. Discord Bot Setup
1. Go to Discord Developer Portal: https://discord.com/developers/applications
2. Create New Application.
3. Navigate to `OAuth2` and ensure your n8n instance's redirect URL is configured (e.g., `https://your-n8n.com/rest/oauth2-credential/callback`).
4. Navigate to `Bot`, then `Add Bot`, and enable "Send Messages" permission.
5. Copy the `Client ID` and `Client Secret`.

### 2. Create Data Table
```
Table Name: Discudemy
Columns:
  - link (string)
  - title (string)
```

### 3. Import Workflow
```bash
# Copy workflow.json content → n8n UI → Import from JSON
```

### 4. Configure Credentials
1. In n8n: Credentials → New → Discord OAuth2 API.
2. Add required credentials:
   - **Client ID**: Paste the Client ID obtained from Discord Developer Portal.
   - **Client Secret**: Paste the Client Secret obtained from Discord Developer Portal.
3. Authorize with Discord.

*Note: workflow.json has redacted credentials for security*

### 5. Update Node References
After import, re-select:
- **Get link**: Select the "Discudemy" table.
- **Insert to Data Table**: Select the "Discudemy" table.
- **Delete Old Data**: Select the "Discudemy" table.
- **Send a message**: Choose your Discord server and channel.

### 6. Test & Activate
```bash
# Test execution first
# Check executions tab for errors
# Toggle "Active" when confirmed working
```

## Troubleshooting

**Problem 1: Workflow fails to send messages to Discord.**
- Symptom: Discord messages are not appearing, and n8n execution logs show errors related to Discord.
- Solution: Verify that the Discord Bot has "Send Messages" permission enabled in the Discord Developer Portal and that the correct Discord server and channel are selected in the "Send a message" node.

**Problem 2: Duplicate courses are being posted.**
- Symptom: The same free course is posted multiple times to Discord.
- Solution: Ensure the "Discudemy" Data Table is correctly configured and selected in the "Get link" and "Insert to Data Table" nodes for proper deduplication.

## Advanced Configuration (Optional)

- **RSS Feed URL**: Modify the RSS Feed Trigger node to monitor a different Discudemy category or a different RSS feed entirely.
- **Retention Policy**: Adjust the "Delete Old Data" node to change the retention period for old course entries in the Data Table.
- **Discord Message Format**: Customize the message content in the "Send a message" node to change how course information is presented in Discord.

