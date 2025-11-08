# Setup Instructions

## Prerequisites
- n8n instance (cloud or self-hosted)
- Discord server with bot permissions

## Discord Bot Setup

1. Go to Discord Developer Portal: https://discord.com/developers/applications
2. Create New Application
3. OAuth2 → Add redirect URL: `https://your-n8n.com/rest/oauth2-credential/callback`
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
1. Credentials → New → Discord OAuth2 API
2. Paste Client ID & Secret
3. Authorize with Discord

### 4. Update Node References
- **Get row(s)**: Select "Discudemy" table
- **Insert row**: Select "Discudemy" table
- **Send a message**: Choose server & channel
- **Delete Old Data**: Select "Discudemy" table

## Test & Activate

\`\`\`bash
# Test execution first
# Then toggle "Active" in n8n UI
\`\`\`

