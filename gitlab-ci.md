---
description: >-
  This guide will help you integrate Scandium into your GitLab CI/CD workflow.
  With just a few steps, you’ll be able to run automated tests from your
  Scandium test suite on every push or  merge request.
---

# GitLab CI

### What You’ll Achieve

By the end of this guide, your GitLab pipeline will:

* Automatically run tests from a Scandium suite on every push or merge request.
* Display test results directly in the GitLab CI logs.

***

### Prerequisites

Before you begin, make sure you have:

* A [Scandium](https://getscandium.com) account with:
  * Your `API_TOKEN`
  * A `PROJECT_ID` and `SUITE_ID`
* A GitLab repository with CI/CD enabled
* A `.gitlab-ci.yml` file in your repository

***

### 🛠️ Step 1: Set Your GitLab CI/CD Variables

1. Go to your GitLab repository.
2. Click **Settings** > **CI/CD** > **Variables**.
3. Add the following variables:

| Variable Name  | Description                                                                                                         |
| -------------- | ------------------------------------------------------------------------------------------------------------------- |
| `API_TOKEN`    | Your Scandium API token                                                                                             |
| `PROJECT_ID`   | Your Scandium project ID                                                                                            |
| `SUITE_ID`     | Your Scandium test suite ID                                                                                         |
| `HUB_URL`      | _(Optional)_ Selenium Grid URL, if running on your infrastructure                                                   |
| `STARTING_URL` | _(Optional)_ The URL your tests should start from. This will override all tests within the suite you are executing. |



***

### 📁 Step 2: Create or Update Your `.gitlab-ci.yml`

Create or update your `.gitlab-ci.yml` file with the following:

```yaml
image: ubuntu:latest

variables:
  BROWSER: "chrome"
  SCREENSHOT: "true"
  VARIABLES: "{}"
  RETRY: "0"
  MAX_ATTEMPTS: "30"
  WAIT_PERIOD: "120"

stages:
  - test

run_scandium_tests:
  stage: test
  script:
    - apt-get update && apt-get install -y curl jq
    - SCRIPT_URL="https://raw.githubusercontent.com/GetScandium/files/refs/heads/main/scandium_script.sh"
    - curl -o scandium_script.sh $SCRIPT_URL
    - chmod +x scandium_script.sh
    - ./scandium_script.sh
  tags:
    - docker
  artifacts:
    paths:
      - test-results/
```



***

### Step 3: Push to Trigger

Once you’ve committed and pushed your `.gitlab-ci.yml` file, GitLab will automatically run the pipeline and execute your Scandium test suite.



***

### Troubleshooting Tips

| Problem                                | Solution                                                                                   |
| -------------------------------------- | ------------------------------------------------------------------------------------------ |
| ❌ `Missing required variable`          | Double-check that `API_TOKEN`, `PROJECT_ID`, and `SUITE_ID` are set in your repo variables |
| ❌ `Script not found or not executable` | Ensure the `SCRIPT_URL` is valid and script has execution permission (`chmod +x`)          |
| 🕒 `Stuck waiting`                     | Adjust `WAIT_PERIOD` and `MAX_ATTEMPTS` in the variable section                            |

***

###
