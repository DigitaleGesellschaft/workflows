# [GitHub Actions workflows](https://docs.github.com/de/actions/reference/workflows-and-actions) for office automation

## Newsletter draft

This workflow runs on the second Sunday of every month. It fetches a response from an AI model via OpenRouter and creates a new page in our [Confluence instance](https://wiki.digitale-gesellschaft.ch/).

### Setup instructions

#### 1. Confluence API token

- Log in to your Atlassian account.
- Go to **Account Settings** > **Security** > **Create and manage API tokens**.
- Create a new token and save it.

#### 2. GitHub secrets

In your GitHub repository, go to **Settings** > **Secrets and variables** > **Actions** and add the following secrets:

| Secret Name | Description | Default |
|-------------|-------------|---------|
| `OPENROUTER_API_KEY` | Your API key from [OpenRouter](https://openrouter.ai/). |
| `CONFLUENCE_DOMAIN` | The subdomain of your Confluence instance (e.g., `mycompany` if your URL is `mycompany.atlassian.net`). |
| `CONFLUENCE_EMAIL` | The email address associated with your Atlassian account. |
| `CONFLUENCE_API_TOKEN` | The API token you generated in step 1. |
| `CONFLUENCE_SPACE_KEY` | The key of the space where you want to create the page (e.g., `AL`, `NOT`, `GES`). Defaults to `GES`. |

#### 3. Workflow configuration

- The workflow is defined in `.github/workflows/monthly_report.yml`.
- It uses a cron schedule `0 0 * * 0` (every Sunday) and then filters for the second Sunday (days 8-14 of the month).
- You can manually trigger the workflow from the **Actions** tab in GitHub for testing.

### Files

- `scripts/ai_to_confluence.sh`: The main script that handles API calls using `curl`.
- `.github/workflows/monthly_report.yml`: The GitHub Action definition.
