---
description: >-
  Automatically execute your Scandium tests within your existing Continuous
  Integration/Continuous Deployment pipeline.
---

# Continuous Integration (CI/CD)

> To interact with the Scandium Cloud Runner API, you need an API token. You can get one from your profile on dashboard.\
> Visit your profile [https://app.getscandium.com/settings/profile](https://playground.getscandium.com/settings/profile) and copy your API token

In order to successfully execute a test case or test suite, you will need following Parameters, in addition to the API TOKEN copied from your profile. Read on for how to get each necessary parameter.

**Project ID**

Click on the projects dropdown, then click on the "View all" button

<figure><img src="../.gitbook/assets/image (19).png" alt=""><figcaption><p>view all projects</p></figcaption></figure>

From the list of projects displayed, click on the options (kebab menu) on the project card, then click on "Copy project id"

<figure><img src="../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption><p>copy project id</p></figcaption></figure>



**Suite ID**

Applicable when you want to run a test suite. To get a test suite's ID, from the suites listing page, find the desired test case, click on its options menu, then click on "Copy suite id"





Check the guides below for specific pipelines:

[azure-devops.md](azure-devops.md "mention")

[bamboo-ci.md](bamboo-ci.md "mention")

[bitbucket-pipelines.md](bitbucket-pipelines.md "mention")

[circle-ci.md](circle-ci.md "mention")

[github-actions.md](github-actions.md "mention")

[gitlab-ci.md](../gitlab-ci.md "mention")

[jenkins.md](../jenkins.md "mention")

[travis-ci.md](../travis-ci.md "mention")
