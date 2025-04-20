---
description: >-
  This guide will help you integrate Scandium into your Azure DevOps pipeline.
  You’ll be able to trigger and monitor Scandium test executions directly within
  your Azure build or release pipelines.
---

# Azure Devops

### What You’ll Achieve

By the end of this guide, your Azure DevOps pipeline will:

* Trigger Scandium test suites.
* Display live results and logs in the pipeline UI.

***

### Prerequisites

Ensure you have:

* A [Scandium](https://getscandium.com) account with:
  * Your `API_TOKEN`
  * A `PROJECT_ID` and `SUITE_ID`
* An Azure DevOps project and pipeline setup
* Basic understanding of YAML-based pipeline configuration

***

### Step 1: Store Secrets in Azure DevOps

1. Go to your project settings in Azure DevOps.
2. Under **Pipelines**, click on **Library**.
3. Create a variable group (e.g., `ScandiumVars`).
4. Add the following secrets and check “Keep this value secret” where applicable:

| Variable Name  | Value / Description                     |
| -------------- | --------------------------------------- |
| `API_TOKEN`    | Your Scandium API token                 |
| `PROJECT_ID`   | Your Scandium project ID                |
| `SUITE_ID`     | Your Scandium test suite ID             |
| `HUB_URL`      | _(Optional)_ Selenium Grid URL          |
| `STARTING_URL` | _(Optional)_ Starting URL for the tests |
| `BROWSER`      | _(Optional)_  `chrome` _(default)_      |
| `SCREENSHOT`   | _(Optional)_  `true` or `false`         |
| `VARIABLES`    | _(Optional)_  `'{}'` _(as JSON string)_ |
| `RETRY`        | _(Optional)_  `0`                       |
| `MAX_ATTEMPTS` | _(Optional)_  `30`                      |
| `WAIT_PERIOD`  | _(Optional)_  `120`                     |

***

### Step 2: Configure Your YAML Pipeline

Add the following tasks to your pipeline YAML file:

```
trigger:
  branches:
    include:
      - main

variables:
  - group: ScandiumVars

pool:
  vmImage: 'ubuntu-latest'

steps:
  - script: sudo apt-get update && sudo apt-get install -y jq
    displayName: 'Install jq'

  - script: |
      SCRIPT_URL="https://raw.githubusercontent.com/GetScandium/files/refs/heads/main/scandium_script.sh"
      curl -o scandium_script.sh $SCRIPT_URL
      chmod +x scandium_script.sh
    displayName: 'Download Scandium Script'

  - script: ./scandium_script.sh
    env:
      API_TOKEN: $(API_TOKEN)
      PROJECT_ID: $(PROJECT_ID)
      SUITE_ID: $(SUITE_ID)
      HUB_URL: $(HUB_URL)
      STARTING_URL: $(STARTING_URL)
      BROWSER: $(BROWSER)
      SCREENSHOT: $(SCREENSHOT)
      VARIABLES: $(VARIABLES)
      RETRY: $(RETRY)
      MAX_ATTEMPTS: $(MAX_ATTEMPTS)
      WAIT_PERIOD: $(WAIT_PERIOD)
    displayName: 'Run Scandium Script'
```

***

### Step 3: Trigger a Pipeline Run

Push code or manually trigger the pipeline from Azure DevOps. You’ll see logs from Scandium directly in your pipeline output.

***

### Troubleshooting Tips

| Problem               | Solution                                                                 |
| --------------------- | ------------------------------------------------------------------------ |
| ❌ Missing environment | Ensure secrets are linked in the variable group and referenced correctly |
| ❌ Script permission   | Ensure `chmod +x` is applied before running the script                   |
| 🕒 Long wait          | Adjust `WAIT_PERIOD` and `MAX_ATTEMPTS`                                  |

***



***
