---
description: >-
  This guide will help you integrate Scandium into your Jenkins pipeline. With
  just a few steps, you’ll be able to run automated tests from your Scandium
  test suite as part of your CI/CD process.
---

# Jenkins

### What You’ll Achieve

By the end of this guide, your Jenkins job will:

* Automatically run tests from a Scandium suite during the build process.
* Display test results directly in Jenkins console output.

***

### Prerequisites

Before you begin, make sure you have:

* A [Scandium](https://getscandium.com) account with:
  * Your `API_TOKEN`
  * A `PROJECT_ID` and `SUITE_ID`
* Jenkins installed and running
* `curl` and `jq` installed on the Jenkins build agent
* A Freestyle project or Pipeline job configured in Jenkins

***

### Step 1: Configure Environment Variables in Jenkins

You can set environment variables in two ways:

#### Option A: Global Jenkins Environment Variables

1. Navigate to **Manage Jenkins** > **Configure System**.
2. Under **Global properties**, check **Environment variables**.
3. Add the following variables:

| Variable Name  | Description                                                                                                         |
| -------------- | ------------------------------------------------------------------------------------------------------------------- |
| `API_TOKEN`    | Your Scandium API token                                                                                             |
| `PROJECT_ID`   | Your Scandium project ID                                                                                            |
| `SUITE_ID`     | Your Scandium test suite ID                                                                                         |
| `HUB_URL`      | _(Optional)_ Selenium Grid URL, if running on your infrastructure                                                   |
| `STARTING_URL` | _(Optional)_ The URL your tests should start from. This will override all tests within the suite you are executing. |



***

### Step 2: Add Build Steps in Jenkins Pipeline

#### If using a **Pipeline Job**, your `Jenkinsfile` should look like this:

```
pipeline {
  agent any

  environment {
    BROWSER = 'chrome'
    SCREENSHOT = 'true'
    VARIABLES = '{}'
    RETRY = '0'
    MAX_ATTEMPTS = '30'
    WAIT_PERIOD = '120'
  }

  stages {
    stage('Checkout Code') {
      steps {
        checkout scm
      }
    }

    stage('Install Dependencies') {
      steps {
        sh 'sudo apt-get update && sudo apt-get install -y curl jq'
      }
    }

    stage('Download Scandium Script') {
      steps {
        sh '''
          SCRIPT_URL="https://raw.githubusercontent.com/GetScandium/files/refs/heads/main/scandium_script.sh"
          curl -o scandium_script.sh $SCRIPT_URL
          chmod +x scandium_script.sh
        '''
      }
    }

    stage('Run Scandium Test') {
      steps {
        sh './scandium_script.sh'
      }
    }
  }
}
```



***

### Step 3: Run Your Jenkins Job

Trigger your Jenkins job manually or on a git push event. Your Scandium test suite will execute as part of the build process.



***

### Troubleshooting Tips

| Problem                                | Solution                                                                         |
| -------------------------------------- | -------------------------------------------------------------------------------- |
| ❌ `Missing required variable`          | Ensure `API_TOKEN`, `PROJECT_ID`, and `SUITE_ID` are set in Jenkins env vars     |
| ❌ `Script not found or not executable` | Double-check the script URL and ensure it has execution permissions (`chmod +x`) |
| 🕒 `Stuck waiting`                     | Adjust `WAIT_PERIOD` and `MAX_ATTEMPTS` in the Jenkinsfile                       |

***

