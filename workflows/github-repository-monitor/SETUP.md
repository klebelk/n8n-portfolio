# Quick Setup (20 minutes)

## Prerequisites
- [x] n8n instance (cloud or self-hosted)
- [x] GitHub account (Personal Access Token may be needed for higher rate limits)
- [x] OpenAI account with API key
- [x] Gmail account
- [x] Slack workspace with permissions to add apps

## Steps

### 1. Create Data Table
```
Table Name: github-releases
Columns:
  - tag_name (string)
  - repo_name (string)
```

### 2. Import Workflow
```bash
# Copy workflow.json content → n8n UI → Import from JSON
```

### 3. Configure Credentials
1. In n8n: Credentials → New → [Service Name]
2. Add required credentials:
   - **GitHub API**: Connect your GitHub account.
   - **OpenAI API**: Add your OpenAI API key.
   - **Gmail OAuth2**: Connect your Gmail account.
   - **Slack OAuth2 API**: Connect your Slack workspace.

*Note: workflow.json has redacted credentials for security*

### 4. Update Node References
After import, re-select:
- **Set Repo List**: Update the code to include the GitHub repositories you want to monitor (e.g., `['n8n-io/n8n', 'openai/openai-node']`).
- **Check If Processed**: Select the "github-releases" Data Table.
- **Mark as Processed**: Select the "github-releases" Data Table.
- **OpenAI Chat Model**: Select your OpenAI credential.
- **Send a message (Gmail)**: Update the `sendTo` email address and select your Gmail credential.
- **Send a message1 (Slack)**: Select your Slack channel and credential.

### 5. Test & Activate
```bash
# Test execution first
# Check executions tab for errors
# Toggle "Active" when confirmed working
```

## Troubleshooting

**Problem 1: GitHub node fails with a rate limit error.**
- Symptom: The workflow fails at the "HTTP Request" or "Get a repository" node with a 403 error.
- Solution: For higher API rate limits, create a GitHub Personal Access Token (PAT) and use it in your GitHub credential in n8n instead of OAuth2.

**Problem 2: AI summarization is inaccurate or fails.**
- Symptom: The OpenAI node returns an error or the summary is low quality.
- Solution: Check that your OpenAI API key is correct and your account has credits. You can also experiment with different models (e.g., `gpt-4o-mini`) or adjust the prompt in the "AI Agent" node for better results.

**Problem 3: Notifications are not being sent.**
- Symptom: The workflow appears to run successfully, but no messages arrive in Gmail or Slack.
- Solution: Double-check the "sendTo" email address in the Gmail node. For Slack, ensure the bot is invited to the channel you are posting to. Verify that the credentials for both services are correctly configured and selected in their respective nodes.

## Advanced Configuration (Optional)

- **Change Schedule**: Modify the "Schedule Trigger" node to run more or less frequently (e.g., every hour, once a day).
- **Customize AI Prompt**: Edit the prompt in the "AI Agent" node to change the tone, length, or format of the AI-generated summaries.
- **Add More Notifiers**: Duplicate the notification nodes to send digests to other platforms like Discord or Microsoft Teams.