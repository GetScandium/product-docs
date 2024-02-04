---
description: >-
  On this page, you will find sample code and ways for integrating Scandium
  tests into come CI/CI pipeline.
---

# CI/CD pipelines

> If your CI/CD pipeline example is not provided on this page, please feel free to reach out to us. You can do so via our [slack channel here](https://join.slack.com/t/scandiumcommunity/shared\_invite/zt-22yqencvp-K2l6IfNsL5ig\~Je4D3nGyA)

### Azure Devops

In Azure DevOps, you can use the "HTTP REST" task to make an API call to the Scandium Cloud Runner. Here's an example of how you can achieve this in an Azure DevOps pipeline using the HTTP REST task.

Please note the following:

1. Replace `<API TOKEN>`, `<PROJECT ID>`, `<SUITE ID>`, and `<YOUR_SERVICE_CONNECTION_NAME>` with your actual API token, project ID, suite ID, and the name of your service connection, respectively.
2. Make sure you have a service connection configured in your Azure DevOps project that has the necessary permissions to make the API call.

This YAML snippet assumes you're using the `HTTP REST` task in Azure DevOps. Ensure that the `HTTP REST` task is available in your organization or project. If not, you might need to install it from the Azure DevOps Marketplace.

Assuming you have stored your API token, project ID, and suite ID as pipeline variables, you can use the following YAML snippet as an example:

```yaml
trigger:
- main

pool:
  vmImage: 'windows-latest'

variables:
  apiToken: '<API TOKEN>'
  projectId: '<PROJECT ID>'
  suiteId: '<SUITE ID>'

steps:
- task: UseDotNet@2
  displayName: 'Use .NET Core sdk'
  inputs:
    version: '3.x'

- task: HttpRest@1
  displayName: 'Make API call - Run E2E test suite'
  inputs:
    connectionType: 'connectedServiceNameARM'
    connectedServiceNameSelector: 'ConnectedServiceName'
    method: 'POST'
    authentication: 'Basic'
    customHeaders: |
      Accept: application/json
      Content-Type: application/json
      x-api-token: $(apiToken)
    endpoint: '<YOUR_SERVICE_CONNECTION_NAME>'  # Replace with the name of your service connection
    urlSuffix: '/suites/execute'
    body: |
      {
          "project_id": "$(projectId)",
          "suite_id": "$(suiteId)",
          "strategy": "await"
      }

```

### Github Actions

In your Github actions workflow, add a job to your YAML file like below:

```yaml
# This is a basic workflow to help you get started with Actions

name: CI with Scandium

# Controls when the workflow will run
on:
  # Triggers the workflow on push or pull request events but only for the "main" branch
  push:
    branches: [ "main" ]
  pull_request:
    branches: [ "main" ]

  # Allows you to run this workflow manually from the Actions tab
  workflow_dispatch:

# A workflow run is made up of one or more jobs that can run sequentially or in parallel
jobs:
  # This workflow contains a single job called "build"
  build:
    # The type of runner that the job will run on
    runs-on: ubuntu-latest

    # Steps represent a sequence of tasks that will be executed as part of the job
    steps:
      # Checks-out your repository under $GITHUB_WORKSPACE, so your job can access it
      - uses: actions/checkout@v3

      - name: Run Scandium Test
        run: |
          response=$(curl -X POST -H "Content-Type: application/json" -H "x-api-token: ${{ vars.API_TOKEN }}" -d '{"project_id": "${{ vars.PROJECT_ID }}", "test_id": "${{ vars.TEST_ID }}","browser": "chrome","screenshot": true,"strategy": "await","variables": {"username": "sdk", "age": 11},"retry": 0}' "https://scr.getscandium.com/tests/execute")
          status=$(echo "$response" | jq -r .data.result.status)
          message=$(echo "$response" | jq -r .message)

          if [ "$status" = "success" ]; then
            echo "Test ran successfully. Status: $status"
          else
            echo "Test ran with failure. Status: $status"
            exit 1
          fi
        env:
          CURL_CA_BUNDLE: /etc/ssl/certs/ca-certificates.crt # Set the CA certificates bundle path

      # - name: Install jq
      #   run: |
      #     sudo apt-get update -y
      #     sudo apt-get install -y jq
```
