# Setup Instructions

## Prerequisites
-   n8n instance (cloud or self-hosted)
-   GitHub account
-   OpenAI account (for AI summarization)
-   Gmail account (for email notifications)
-   Slack workspace (for Slack notifications)

## n8n Setup

### 1. Create Data Table
Create an n8n Data Table to store processed GitHub releases for deduplication.

```
Name: github-releases
Columns:
  - tag_name (string)
  - repo_name (string)
```

### 2. Import Workflow
Import the `workflow.json` content into your n8n instance.

```bash
# Copy workflow.json content → n8n UI → Workflows → New → Import from JSON
```

### 3. Configure Credentials
Create and configure the following credentials in your n8n instance:

-   **GitHub API**: Connect your GitHub account.
    *Note: The `workflow.json` has redacted credential references. You will need to link this credential to the 'Get a repository' node after importing.* 

-   **OpenAI API**: Connect your OpenAI account.
    *Note: Link this credential to the 'OpenAI Chat Model' node after importing.* 

-   **Gmail OAuth2**: Connect your Gmail account.
    *Note: Link this credential to the 'Send a message' (Gmail) node after importing.* 

-   **Slack OAuth2 API**: Connect your Slack workspace.
    *Note: Link this credential to the 'Send a message1' (Slack) node after importing.* 

### 4. Update Node References
After importing the workflow, you will need to re-select or configure the following in the n8n UI, as their IDs are redacted in the `workflow.json` for security:

-   **Set Repo List**: Update the `jsCode` to include the GitHub repositories you wish to monitor (e.g., `['owner/repo1', 'owner/repo2']`).
-   **Get a repository**: Ensure the GitHub credential is linked.
-   **Check If Processed**: Select the "github-releases" Data Table.
-   **Mark as Processed**: Select the "github-releases" Data Table.
-   **OpenAI Chat Model**: Select your OpenAI credential and the desired model (e.g., `gpt-4o-mini`).
-   **Send a message (Gmail)**: Update the `sendTo` email address and ensure the Gmail credential is linked.
-   **Send a message1 (Slack)**: Select your Slack channel and ensure the Slack credential is linked.

## Test & Activate

```bash
# Test execution first to ensure everything is configured correctly.
# Then toggle "Active" in the n8n UI to enable scheduled monitoring.
```