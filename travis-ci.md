---
description: >-
  This guide will help you integrate Scandium into your Travis CI pipeline. With
  just a few steps, you’ll be able to run automated tests from your Scandium
  test suite every time you push code.
---

# Travis CI

### What You’ll Achieve

By the end of this guide, your Travis CI pipeline will:

* Automatically run tests from a Scandium suite on every push to your repository.
* Display test results directly in the Travis CI logs.

***

### Prerequisites

Before you begin, make sure you have:

* A [Scandium](https://getscandium.com) account with:
  * Your `API_TOKEN`
  * A `PROJECT_ID` and `SUITE_ID`
* Access to a GitHub repository connected to Travis CI
* A `.travis.yml` file or familiarity with configuring one

***

### Step 1: Set Your Travis Environment Variables

1. Navigate to your project on [Travis CI](https://travis-ci.com/).
2. Go to **More Options > Settings**.
3. Under **Environment Variables**, add the following:

| Variable Name  | Description                                                                                                         |
| -------------- | ------------------------------------------------------------------------------------------------------------------- |
| `API_TOKEN`    | Your Scandium API token                                                                                             |
| `PROJECT_ID`   | Your Scandium project ID                                                                                            |
| `SUITE_ID`     | Your Scandium test suite ID                                                                                         |
| `HUB_URL`      | _(Optional)_ Selenium Grid URL, if running on your infrastructure                                                   |
| `STARTING_URL` | _(Optional)_ The URL your tests should start from. This will override all tests within the suite you are executing. |

### Step 2: Update Your `.travis.yml`

Add the following to your `.travis.yml` file:

```yaml
language: bash

os:
  - linux

dist: focal

before_install:
  - sudo apt-get update
  - sudo apt-get install -y jq curl

script:
  - |
    SCRIPT_URL="https://raw.githubusercontent.com/GetScandium/files/refs/heads/main/scandium_script.sh"
    curl -o scandium_script.sh $SCRIPT_URL
    chmod +x scandium_script.sh
    ./scandium_script.sh

env:
  global:
    - BROWSER=chrome
    - SCREENSHOT=true
    - VARIABLES='{}'
    - RETRY=0
    - MAX_ATTEMPTS=30
    - WAIT_PERIOD=120
```

### Push to Trigger

Once you've pushed this `.travis.yml` to your repo, Travis will automatically run the pipeline, and your Scandium tests will execute.

### Troubleshooting Tips

| Problem                                | Solution                                                                               |
| -------------------------------------- | -------------------------------------------------------------------------------------- |
| ❌ `Missing required variable`          | Double-check that `API_TOKEN`, `PROJECT_ID`, and `SUITE_ID` are set in Travis settings |
| ❌ `Script not found or not executable` | Ensure the `SCRIPT_URL` is valid and script has execution permission (`chmod +x`)      |
| 🕒 `Stuck waiting`                     | Adjust `WAIT_PERIOD` and `MAX_ATTEMPTS` in the environment variables                   |
