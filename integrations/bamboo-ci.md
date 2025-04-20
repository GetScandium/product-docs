---
description: >-
  This guide will help you integrate Scandium into your Bamboo CI pipeline. With
  a few configuration tweaks, you can trigger your automated tests from a
  Scandium suite directly within your build plans.
---

# Bamboo CI

### What You’ll Achieve

By the end of this guide, your Bamboo build will:

* Run Scandium test suites as part of your build plan.
* Display test output in your Bamboo build logs.

***

### Prerequisites

Before you begin, make sure you have:

* A [Scandium](https://getscandium.com) account with:
  * Your `API_TOKEN`
  * A `PROJECT_ID` and `SUITE_ID`
* Bamboo CI installed and running
* Administrator access to create/edit build plans
* An agent that has `curl`, `bash`, and `jq` installed

***

### Step 1: Define Variables in Bamboo

In your build plan:

1. Navigate to your plan configuration.
2. Click **Actions** > **Configure Plan**.
3. Go to **Variables** and define the following:

| Variable Name  | Value / Description                                  |
| -------------- | ---------------------------------------------------- |
| `API_TOKEN`    | Your Scandium API token                              |
| `PROJECT_ID`   | Your Scandium project ID                             |
| `SUITE_ID`     | Your Scandium test suite ID                          |
| `HUB_URL`      | _(Optional)_ Selenium Grid URL                       |
| `STARTING_URL` | _(Optional)_ Starting URL for the tests              |
| `BROWSER`      | _(Optional)_ `chrome` _(default)_                    |
| `SCREENSHOT`   | _(Optional)_ `true` or `false`                       |
| `VARIABLES`    | _(Optional)_ `'{}'` _(as JSON string)_               |
| `RETRY`        | _(Optional)_ Number of retries on failure, e.g. `0`  |
| `MAX_ATTEMPTS` | _(Optional)_ Max polling attempts, e.g. `30`         |
| `WAIT_PERIOD`  | _(Optional)_ Polling interval in seconds, e.g. `120` |



***

### Step 2: Add Script Tasks to Run Scandium

In your build stage:

1. Add a **Script** task named `Install Dependencies`
   * Script Body:

```
sudo apt-get update && sudo apt-get install -y jq
```

2. Add another **Script** task named `Download Scandium Script`
   * Script Body:

```
SCRIPT_URL="https://raw.githubusercontent.com/GetScandium/files/refs/heads/main/scandium_script.sh"
curl -o scandium_script.sh $SCRIPT_URL
chmod +x scandium_script.sh
```

3. Add a **Script** task named `Run Scandium Script`
   * Script Body:

```
./scandium_script.sh
```

***

### Step 3: Trigger a Build

You can now trigger your Bamboo plan manually or via a VCS change. Watch the build logs for test output and status.

***

### Troubleshooting Tips

| Problem                       | Solution                                                                              |
| ----------------------------- | ------------------------------------------------------------------------------------- |
| ❌ `Missing required variable` | Make sure required plan variables are defined (`API_TOKEN`, `PROJECT_ID`, `SUITE_ID`) |
| ❌ `Permission denied`         | Ensure the script has execute permission (`chmod +x`)                                 |
| 🕒 `Stuck waiting`            | Adjust `WAIT_PERIOD` and `MAX_ATTEMPTS` plan variables                                |

***



***
