---
description: >-
  This guide will help you integrate Scandium into your GitHub CI/CD pipeline
  using GitHub Actions. With just a few steps, you’ll be able to run automated
  tests from your Scandium test suite every time
---

# Github Actions

### What You’ll Achieve

By the end of this guide, your GitHub workflow will:

* Automatically run tests from a Scandium suite on every push to a chosen branch.
* Optionally allow manual runs from the GitHub Actions UI.
* Show test results directly in your GitHub Actions logs.

***

### Prerequisites

Before you begin, make sure you have:

* A [Scandium](https://getscandium.com) account with:
  * Your `API_TOKEN`
  * A `PROJECT_ID` and `SUITE_ID`
* Access to a GitHub repository
* A basic understanding of how GitHub Actions works

***

### Step 1: Set Your GitHub Secrets

1. Navigate to your repository on GitHub.
2. Go to **Settings > Secrets and variables > Actions > Repository secrets**.
3. Add the following secrets:

| **Secret Name** | **Description**                                                                                                     |
| --------------- | ------------------------------------------------------------------------------------------------------------------- |
| `API_TOKEN`     | Your Scandium API token                                                                                             |
| `PROJECT_ID`    | Your Scandium project ID                                                                                            |
| `SUITE_ID`      | Your Scandium test suite ID                                                                                         |
| `HUB_URL`       | _(Optional)_ Selenium Grid URL, if running on your infrastructure                                                   |
| `STARTING_URL`  | _(Optional)_ The URL your tests should start from. This will override all tests within the suite you are executing. |

### Step 2: Create Your GitHub Actions Workflow

In your repo, create a file at:\
`.github/workflows/run-scandium.yml`

Paste the following:

```yaml
//yaml file
name: Run Scandium Script

on:
  workflow_dispatch:  # Allows manual trigger of the workflow
  push:               # Runs on push to a specific branch
    branches:
      - bashci        # Change this to your desired branch

jobs:
  execute-scandium-script:
    runs-on: ubuntu-latest

    env:
      API_TOKEN: ${{ secrets.API_TOKEN }}
      PROJECT_ID: ${{ secrets.PROJECT_ID }}
      HUB_URL: ${{ secrets.HUB_URL }}
      STARTING_URL: ${{ secrets.STARTING_URL }}
      SUITE_ID: ${{ secrets.SUITE_ID }}
      BROWSER: chrome
      SCREENSHOT: true
      VARIABLES: '{}'
      RETRY: 0
      MAX_ATTEMPTS: 30
      WAIT_PERIOD: 120

    steps:
      - name: Checkout Repository
        uses: actions/checkout@v3

      - name: Install jq
        run: |
          sudo apt-get update
          sudo apt-get install -y jq

      - name: Download the Scandium Bash Script
        run: |
          SCRIPT_URL="https://raw.githubusercontent.com/GetScandium/files/refs/heads/main/scandium_script.sh"
          curl -o scandium_script.sh $SCRIPT_URL
          chmod +x scandium_script.sh

      - name: Run the Scandium Script
        run: |
          ./scandium_script.sh
```

### Step 3: Trigger the Workflow

#### Option 1: Automatic Trigger

Any time you push to the configured branch (e.g., `bashci`), the workflow will run automatically.

#### Option 2: Manual Trigger

Go to your repo on GitHub:

1. Click the **Actions** tab.
2. Select `Run Scandium Script`.
3. Click **Run workflow**.

### Troubleshooting Tips

| **Problem**                            | **Solution**                                                                             |
| -------------------------------------- | ---------------------------------------------------------------------------------------- |
| ❌ `Missing required variable`          | Double-check that `API_TOKEN`, `PROJECT_ID`, and `SUITE_ID` are set correctly as secrets |
| ❌ `Script not found or not executable` | Ensure the `SCRIPT_URL` is valid and script has execution permission (`chmod +x`)        |
| 🕒 `Stuck waiting`                     | Adjust `WAIT_PERIOD` and `MAX_ATTEMPTS` in the environment variables                     |
