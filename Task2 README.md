# Task 2 – n8n GitHub AI Repository Monitoring Workflow

## Overview

This n8n workflow runs on a scheduled trigger and retrieves the top 5 GitHub repositories related to artificial intelligence based on star count.

It selects the top repository, retrieves its GitHub README through the GitHub API, transforms the data, checks whether the repository has more than 100,000 stars, and sends a notification to Discord when the condition is satisfied.

## Workflow

Schedule Trigger
→ GitHub Search API
→ Code: Transform Top 5
→ Limit: Select Top Repository
→ GitHub README API
→ Code: Process README
→ IF: Stars > 100,000
→ Discord Notification

An error-handling branch is also configured for the initial GitHub API request.

## APIs Used

- GitHub Search API – retrieves AI-related repositories.
- GitHub Repository README API – retrieves README information for the selected repository.
- Discord – sends the final notification.

## Transformation

The workflow extracts:
- Repository name
- Full repository name
- Stars
- Forks
- Programming language
- Description
- GitHub URL
- README preview

The README returned by GitHub is Base64 encoded, so the workflow decodes it before generating the preview.

## Condition

The IF node checks:

`stars > 100000`

This threshold is used as a demonstration condition for the workflow branch.

If the condition is true, a Discord notification is sent.

## Error Handling

The initial GitHub API request is configured with:

`Continue (using error output)`

If the request fails, the error information is passed to a separate Code node. The error is formatted and sent to Discord so that the failure is visible instead of being silently ignored.

## Credentials

Discord authentication is handled through n8n's credential system. Authentication secrets are not hard-coded into the workflow logic.

## Testing

The workflow was executed successfully and produced a Discord notification containing the repository information.

Example successful output:
- Repository: AutoGPT
- Stars: 187620
- Forks: 45982
- Language: Python

## Files

- `Task2_Workflow_Shreyas_Anand_Bakshi.json` – exported n8n workflow
- `screenshots/workflow-canvas.png` – workflow structure
- `screenshots/successful-execution.png` – successful execution/output
