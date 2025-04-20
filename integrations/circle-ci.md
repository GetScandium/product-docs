---
description: >-
  This guide will help you integrate Scandium into your CircleCI workflow. With
  just a few steps, you’ll be able to run automated tests from your Scandium
  test suite on every push or pull request.
---

# Circle CI

### What You’ll Achieve

By the end of this guide, your CircleCI pipeline will:

* Automatically run tests from a Scandium suite on every push.
* Display test results directly in the CircleCI logs.

***

### Prerequisites

Before you begin, make sure you have:

* A [Scandium](https://getscandium.com) account with:
  * Your `API_TOKEN`
  * A `PROJECT_ID` and `SUITE_ID`
* A CircleCI project connected to your repository
* A `.circleci/config.yml` file in your project root

***

### Step 1: Set Your CircleCI Environment Variables

1. Go to your CircleCI project dashboard.
2. Navigate to **Project Settings** > **Environment Variables**.
3. Add the following environment variables:

| Variable Name  | Description                                                                                                         |
| -------------- | ------------------------------------------------------------------------------------------------------------------- |
| `API_TOKEN`    | Your Scandium API token                                                                                             |
| `PROJECT_ID`   | Your Scandium project ID                                                                                            |
| `SUITE_ID`     | Your Scandium test suite ID                                                                                         |
| `HUB_URL`      | _(Optional)_ Selenium Grid URL, if running on your infrastructure                                                   |
| `STARTING_URL` | _(Optional)_ The URL your tests should start from. This will override all tests within the suite you are executing. |



***

### Step 2: Create or Update `.circleci/config.yml`

Create or update your `.circleci/config.yml` file with the following configuration:

```yaml
version: 2.1

jobs:
  run-scandium-tests:
    docker:
      - image: cimg/base:stable
    environment:
      BROWSER: "chrome"
      SCREENSHOT: "true"
      VARIABLES: "{}"
      RETRY: "0"
      MAX_ATTEMPTS: "30"
      WAIT_PERIOD: "120"
    steps:
      - checkout
      - run:
          name: Install Dependencies
          command: sudo apt-get update && sudo apt-get install -y curl jq
      - run:
          name: Download Scandium Script
          command: |
            SCRIPT_URL="https://raw.githubusercontent.com/GetScandium/files/refs/heads/main/scandium_script.sh"
            curl -o scandium_script.sh $SCRIPT_URL
            chmod +x scandium_script.sh
      - run:
          name: Run Scandium Script
          command: ./scandium_script.sh

workflows:
  version: 2
  test:
    jobs:
      - run-scandium-tests
```



***

### Step 3: Commit and Push

Once you’ve committed and pushed your `.circleci/config.yml` file, CircleCI will automatically trigger the workflow and execute your Scandium test suite.



***

### Troubleshooting Tips

| Problem                                | Solution                                                                                   |
| -------------------------------------- | ------------------------------------------------------------------------------------------ |
| ❌ `Missing required variable`          | Ensure `API_TOKEN`, `PROJECT_ID`, and `SUITE_ID` are set in CircleCI environment variables |
| ❌ `Script not found or not executable` | Double-check the script URL and ensure you added execution permissions (`chmod +x`)        |
| 🕒 `Stuck waiting`                     | Adjust `WAIT_PERIOD` and `MAX_ATTEMPTS` in the config file                                 |

***

###

***
