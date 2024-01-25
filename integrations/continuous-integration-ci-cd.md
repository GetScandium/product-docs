---
description: >-
  Automatically execute your Scandium tests within your existing Continuous
  Integration/Continuous Deployment pipeline.
---

# Continuous Integration (CI/CD)

By using the Scandium REST API, you can execute your e2e test cases and suites from within any of the several popular CI/CD platforms.

## Execute a test

Calling this endpoint allows you to immediately run a single test case.

### Request

Method: POST

URL: https://scr.getscandium.com/tests/execute

Payload (Body Parameters)

{% hint style="info" %}
Body parameter is expected in JSON format
{% endhint %}

|             |          |                                                                                                                                                                                                                                                                                                                                                                        |
| ----------- | -------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| project\_id | required | The ID of the project containing the test. This can be copied from your dashboard                                                                                                                                                                                                                                                                                      |
| test\_id    | required | The ID of the test to execute. This can be gotten from the test page                                                                                                                                                                                                                                                                                                   |
| browser     | optional | <p>The browser to run this test on. Allow valued: <code>chrome</code> , <code>firefox</code> and <code>edge</code>.<br>If this value is not supplied, the default browser on the test </p><p>case will be used.</p>                                                                                                                                                    |
| strategy    | optional | <p><code>await</code> or <code>callback</code> <br>Use <code>await</code> to make your runner wait until the test done executing (This can make the request take a long while before returning, depending on the length of the test case). Use <code>callback</code> to return immediately (without the result of the run).<br>Default value is <code>await</code></p> |
| variables   | optional | A JSON object of key:value pairs that can be used to set or override existing global variables used in your test                                                                                                                                                                                                                                                       |
| retry       | optional | Specify the number of times you want Scandium to retry a test if it fails. Default is 0. Higher values will increase the time it takes your test to run.                                                                                                                                                                                                               |
| screenshot  | optional | <p><code>true</code> or <code>false</code><br>To determine if screenshots should be taken for each step in the run.<br>Note: screenshot will always be taken for a failed step in the test.</p>                                                                                                                                                                        |



#### Sample request using CURL

```
curl --location 'https://scr.getscandium.com/tests/execute' \
--header 'Accept: application/json' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer <API KEY>' \
--data '{
    "project_id": "<PROJECT ID>",
    "test_id": "<PROJECT ID>",
    "browser": "chrome",
    "screenshot": true,
    "strategy": "callback",
    "variables": {"username": "sdk", "age": 11},
    "retry": 0
}'
```



#### Sample Response (success)

```json
{
    "data": {
        "result": {
            "id": "9b034f22-8e0b-4e05-8971-61f81d7bd48a",
            "starting_url": "https://demoqa.com/automation-practice-form",
            "source": "remote",
            "browser": "chrome",
            "browser_version": "117.0.5938.132",
            "operating_system": "linux",
            "operating_system_version": "",
            "is_mobile": false,
            "duration": 91667,
            "started_at": 1705931602516,
            "finished_at": 1705931694183,
            "status": "success",
            "running_status": "completed",
            "test_id": "9b034f22-8e0b-4e05-8971-61f81d7bd48a",
            "name": "quick demoqa",
            "reason": "Test completed",
            "summary": {
                "total": 34,
                "passed": 34,
                "failed": 0,
                "skipped": 0,
                "ignored": 0
            }
        },
        "errors": []
    },
    "message": "Test run completed"
}
```
