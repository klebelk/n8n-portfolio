# GitHub Repository Monitor

## Overview
Automated workflow that monitors specified GitHub repositories for new releases, summarizes their release notes using AI, and sends digests via email (Gmail) and Slack.

## Problem Solved
Keeping track of new releases across multiple GitHub repositories can be challenging. This workflow automates the process of fetching, summarizing, and distributing release information, ensuring you stay updated without manual effort.

## Features
- ✅ Scheduled monitoring of multiple GitHub repositories
- ✅ Fetches latest release information
- ✅ Deduplication of releases using a Data Table
- ✅ AI-powered summarization of release notes (using OpenAI)
- ✅ Generates HTML digest for email (Gmail)
- ✅ Generates Markdown digest for Slack

## Workflow Logic

```
Schedule Trigger → Set Repo List → Loop Over Items → Get a repository → HTTP Request (Latest Release) → Extract Release Info → Check If Processed (Data Table)
                                                                                                                                ↓
                                                                                                                                If (New Release?)
                                                                                                                                ↓
                                                                                                                                Mark as Processed (Data Table) → AI Agent (Summarize Release Notes) → Merge AI Summary → Aggregate All Releases
                                                                                                                                                                                                                          ↓
                                                                                                                                                                                                                          Format Digest (HTML) → Send Email (Gmail)
                                                                                                                                                                                                                          ↓
                                                                                                                                                                                                                          Format Digest (Markdown) → Send Message (Slack)
```

## Key Nodes

1.  **Schedule Trigger**: Initiates the workflow periodically.
2.  **Set Repo List**: Defines the list of GitHub repositories to monitor.
3.  **Loop Over Items**: Iterates through each repository in the list.
4.  **Get a repository**: Fetches general information about the GitHub repository.
5.  **HTTP Request**: Retrieves the latest release data from GitHub API.
6.  **Extract Release Info**: Parses the raw release data, cleans up release notes, and prepares it for further processing.
7.  **Check If Processed**: Queries an n8n Data Table (`github-releases`) to prevent duplicate notifications for already processed releases.
8.  **If**: Branches the workflow based on whether a release is new or already processed.
9.  **Mark as Processed**: Records new release information in the `github-releases` Data Table.
10. **AI Agent**: Utilizes an OpenAI model to generate concise summaries of the release notes.
11. **OpenAI Chat Model**: The underlying large language model used by the AI Agent.
12. **Merge AI Summary to Metadata**: Integrates the AI-generated summary with the release's metadata.
13. **Aggregate**: Collects all processed release data for digest generation.
14. **Format Digest - HTML**: Formats the aggregated release information into an HTML email digest.
15. **Format Digest - mrkdown**: Formats the aggregated release information into a Markdown message for Slack.
16. **Send a message (Gmail)**: Sends the HTML digest via Gmail.
17. **Send a message1 (Slack)**: Sends the Markdown digest via Slack.

## Technical Highlights

### Multi-Repository Monitoring
Configurable list of GitHub repositories to track, allowing for centralized monitoring.

### Deduplication System
Uses an n8n Data Table to store processed release tags, ensuring that notifications are sent only for new releases.

### AI-Powered Summarization
Integrates with OpenAI to provide concise, categorized summaries of release notes, saving time on reading full changelogs.

### Flexible Notifications
Supports sending release digests to both email (Gmail) and Slack, catering to different communication preferences.

## Portfolio Value
Demonstrates: Scheduled automation, API integration (GitHub, OpenAI, Gmail, Slack), data persistence (n8n Data Tables), conditional logic, data transformation, AI/LLM integration, and robust notification systems.