# 📊 Daily Repo Report Action

A reusable GitHub Action that generates a daily summary of activity (Commits, Issues, and Pull Requests) across multiple repositories and sends a beautifully formatted Markdown report directly to your inbox. 

Perfect for keeping track of your portfolio projects, monitoring team activity, or getting a daily digest of your open-source contributions.

## ✨ Features

- **Multi-Repository Support:** Track one or multiple repositories at once.
- **Automated Email Delivery:** Receives the daily summary straight in your email.
- **Visual Job Summaries:** Automatically generates a GitHub Actions Job Summary in your dashboard.
- **Native CLI Integration:** Powered by the official GitHub CLI (`gh api`) for fast and reliable data extraction.

---

## 🚀 Usage

To use this action, you need to create a workflow file in the repository where you want the action to run (e.g., `.github/workflows/daily-report.yml`).

### 1. Configure your Email Password
For security reasons, never hardcode your email password. 
1. Go to your repository's **Settings > Secrets and variables > Actions**.
2. Click **New repository secret**.
3. Name it `EMAIL_PASSWORD` and paste your email app password. *(Note: If using Gmail, you must generate an [App Password](https://support.google.com/accounts/answer/185833)).*

### 2. Add the Workflow File
Copy the following template and adjust the variables to fit your needs:

```yaml
name: Send Daily Report

on:
  schedule:
    # Runs at 17:00 UTC, Monday through Friday
    - cron: '0 17 * * 1-5'
  workflow_dispatch: 

jobs:
  generate-and-send:
    runs-on: ubuntu-latest
    permissions:
      contents: read
      issues: read
      pull-requests: read
      
    steps:
      - name: Run Daily Repo Report
        uses: your-github-username/daily-repo-report-action@main
        with:
          # GitHub Data Configuration
          github-token: ${{ secrets.GITHUB_TOKEN }}
          repositories: 'your-username/project-1, your-username/project-2'
          
          # Email Configuration
          email-to: 'destination@example.com'
          smtp-server: 'smtp.gmail.com'
          smtp-port: '465'
          smtp-username: 'sender@example.com'
          smtp-password: ${{ secrets.EMAIL_PASSWORD }}
```

---

## ⚙️ Inputs

| Input | Required | Description | Example |
| :--- | :---: | :--- | :--- |
| `github-token` | Yes | Token used to authenticate with the GitHub API. | `${{ secrets.GITHUB_TOKEN }}` |
| `repositories` | Yes | Comma-separated list of repositories to track. | `user/repo1, user/repo2` |
| `email-to` | Yes | The email address where the report will be sent. | `boss@company.com` |
| `smtp-server` | Yes | Your email provider's SMTP server address. | `smtp.gmail.com` |
| `smtp-port` | Yes | Your email provider's SMTP port. | `465` (SSL) or `587` (TLS) |
| `smtp-username` | Yes | The email address sending the report. | `bot@company.com` |
| `smtp-password` | Yes | The password for the sending email. (Passed via Secrets). | `${{ secrets.EMAIL_PASSWORD }}` |
---

Created by [gabrielabellan](https://github.com/gabrielabellan) as part of a DevOps/Automation portfolio.
