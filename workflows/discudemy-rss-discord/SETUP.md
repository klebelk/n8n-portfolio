# Setup Instructions

## Prerequisites
- n8n instance (cloud or self-hosted)
- Discord server with bot permissions

## Discord Bot Setup

1. Go to Discord Developer Portal: https://discord.com/developers/applications
2. Create New Application
3. OAuth2 → Ensure your n8n instance's redirect URL is configured (e.g., `https://your-n8n.com/rest/oauth2-credential/callback`)
4. Bot → Add Bot → Enable "Send Messages" permission
5. Copy Client ID & Secret

## n8n Setup

### 1. Create Data Table
\`\`\`
Name: Discudemy
Columns:
  - link (string)
  - title (string)
\`\`\`

### 2. Import Workflow
\`\`\`bash
# Copy workflow.json content → n8n → Import from JSON
\`\`\`

### 3. Configure Credentials
1. In your n8n instance, go to Credentials → New → Discord OAuth2 API.
2. Paste your Client ID & Secret obtained from the Discord Developer Portal.
3. Authorize with Discord.

*Note: The `workflow.json` file has its credential references redacted for security. You will need to link the newly created Discord credential to the 'Send a message' node after importing the workflow.*

### 4. Update Node References
After importing the workflow, you will need to re-select the following in the n8n UI, as their IDs are redacted in the `workflow.json` for security:
-   **Get link**: Select the "Discudemy" table.
-   **Insert to Data Table**: Select the "Discudemy" table.
-   **Delete Old Data**: Select the "Discudemy" table.
-   **Send a message**: Choose your Discord server and channel.

## Test & Activate

\`\`\`bash
# Test execution first
# Then toggle "Active" in n8n UI
\`\`\`

