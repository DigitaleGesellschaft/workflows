# [GitHub Actions workflows](https://docs.github.com/de/actions/reference/workflows-and-actions) for office automation

## Newsletter draft

This workflow runs on the second Wednesday of every month. It fetches a response from an AI model via OpenRouter and creates a new page in our [Confluence instance](https://wiki.digitale-gesellschaft.ch/).

### Setup instructions

#### 1. Confluence API token

- Log in to your Atlassian account.
- Go to **Account Settings** > **Security** > **Create and manage API tokens**.
- Create a new token and save it.

#### 2. GitHub secrets

In your GitHub repository, go to **Settings** > **Secrets and variables** > **Actions** and add all the environment variables listed in the [`scripts/newsletter_draft.sh`](scripts/newsletter_draft.sh) header as secrets.

#### 3. Workflow configuration

- The workflow is defined in [`.github/workflows/newsletter_draft.yml`](.github/workflows/newsletter_draft.yml).
- It executes the Bash script [`scripts/newsletter_draft.sh`](scripts/newsletter_draft.sh).
- It uses a cron schedule [`0 0 * * 3`](.github/workflows/newsletter_draft.yml#L7) (every Wednesday) and then filters for the second Wednesday (days 8-14 of the month).
- It can be manually triggered from the [**Actions** tab](https://github.com/DigitaleGesellschaft/workflows/actions/workflows/newsletter_draft.yml) in GitHub (e.g. for testing).
