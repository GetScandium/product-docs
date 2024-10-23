---
description: >-
  Automatically execute your Scandium tests within your existing Continuous
  Integration/Continuous Deployment pipeline.
---

# Continuous Integration (CI/CD)

By using the Scandium REST API, you can execute your e2e test cases and suites from within any of the several popular CI/CD platforms.

> To interact with the Scandium Cloud Runner API, you need an API token. You can get one from your profile on dashboard.\
> Visit your profile [https://app.getscandium.com/settings/profile](https://playground.getscandium.com/settings/profile) and copy your API token

In order to successfully execute a test case or test suite, you will need following Parameters, in addition to the API TOKEN copied from your profile. Read on for how to get each necessary parameter.

**Project ID**

Click on the projects dropdown, then click on the "View all" button

<figure><img src="../.gitbook/assets/image (19).png" alt=""><figcaption><p>view all projects</p></figcaption></figure>

From the list of projects displayed, click on the options (kebab menu) on the project card, then click on "Copy project id"

<figure><img src="../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption><p>copy project id</p></figcaption></figure>

**Test ID**

Applicable when you want to run a single test case. To get a test case's ID, from the tests listing page, find the desired test case, click on its options menu, then click on "Copy test Id"

<figure><img src="../.gitbook/assets/image (2) (1) (1) (1).png" alt=""><figcaption><p>copy test id</p></figcaption></figure>

**Suite ID**

Applicable when you want to run a test suite. To get a test suite's ID, from the suites listing page, find the desired test case, click on its options menu, then click on "Copy suite id"

## Execute a test

Calling this endpoint allows you to immediately run a single test case.

### Request

## Run a single test case

<mark style="color:green;">`POST`</mark> `https://scr.getscandium.com/tests/execute`

Body parameter is expected in JSON format

#### Headers

| Name                                           | Type   | Description      |
| ---------------------------------------------- | ------ | ---------------- |
| x-api-token<mark style="color:red;">\*</mark>  | String | API TOKEN        |
| Content-Type<mark style="color:red;">\*</mark> | String | application/json |

#### Request Body

| Name                                          | Type    | Description                                                                                                                                                                                                                                                                                                                                                            |
| --------------------------------------------- | ------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| project\_id<mark style="color:red;">\*</mark> | String  | The ID of the project containing the test. This can be copied from your dashboard                                                                                                                                                                                                                                                                                      |
| test\_id<mark style="color:red;">\*</mark>    | String  | The ID of the test to execute. This can be gotten from the test page                                                                                                                                                                                                                                                                                                   |
| browser                                       | String  | <p>The browser to run this test on. Allow valued: <code>chrome</code> , <code>firefox</code> and <code>edge</code>.<br>If this value is not supplied, the default browser on the test </p><p>case will be used.</p>                                                                                                                                                    |
| strategy                                      | String  | <p><code>await</code> or <code>callback</code> <br>Use <code>await</code> to make your runner wait until the test done executing (This can make the request take a long while before returning, depending on the length of the test case). Use <code>callback</code> to return immediately (without the result of the run).<br>Default value is <code>await</code></p> |
| variables                                     | String  | A JSON object of key:value pairs that can be used to set or override existing global variables used in your test                                                                                                                                                                                                                                                       |
| screenshot                                    | Boolean | <p><code>true</code> or <code>false</code><br>To determine if screenshots should be taken for each step in the run.<br>Note: screenshot will always be taken for a failed step in the test.</p>                                                                                                                                                                        |

{% tabs %}
{% tab title="200: OK " %}
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
{% endtab %}
{% endtabs %}



#### Sample request using CURL

```
curl --location 'https://scr.getscandium.com/tests/execute' \
--header 'Accept: application/json' \
--header 'Content-Type: application/json' \
--header 'x-api-token: <API TOKEN' \
--data '{
    "project_id": "<PROJECT ID>",
    "test_id": "<TEST ID>",
    "browser": "chrome",
    "screenshot": true,
    "strategy": "callback",
    "variables": {"username": "sdk", "age": 11},
    "retry": 0
}'
```





## Execute a test suite

Calling this endpoint allows you to immediately run a test suite. _A test suite is a collection of multiple test cases grouped for similar purposes_.

{% hint style="info" %}
**Note:** Executing test suites can take a long time to complete especially if there are so many test cases within the suite, and also depending on the load on our systems at the time of run. Your suite run time will also be affected if you setup multiple execution environments for the suite, as the suite will run all tests for each environment.

&#x20;We’d suggest programming your request to deal with response times up to 10 minutes. If all the suite’s tests are not completed within 10 minutes, the API will send a timeout error (although your tests will still be running in the background).
{% endhint %}

### Request

<mark style="color:green;">`POST`</mark> `https://scr.getscandium.com/suites/execute`

#### Headers

| Name                                           | Type             | Description |
| ---------------------------------------------- | ---------------- | ----------- |
| x-api-token<mark style="color:red;">\*</mark>  | String           | API TOKEN   |
| Content-Type<mark style="color:red;">\*</mark> | application/json |             |

#### Request Body

| Name                                          | Type   | Description                                                                                                                                                                                                                                                                                                                                                             |
| --------------------------------------------- | ------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| project\_id<mark style="color:red;">\*</mark> | String | The ID of the project containing the test. This can be copied from your dashboard                                                                                                                                                                                                                                                                                       |
| suite\_id<mark style="color:red;">\*</mark>   | String | The ID of the suite to execute. This can be gotten from the test page                                                                                                                                                                                                                                                                                                   |
| strategy                                      | String | <p><code>await</code> or <code>callback</code> <br>Use <code>await</code> to make your runner wait until the suite done executing (This can make the request take a long while before returning, depending on the length of the test case). Use <code>callback</code> to return immediately (without the result of the run).<br>Default value is <code>await</code></p> |
| retry                                         | String | Specify the number of times you want a failed test within the suite to be retried. Default is 0. Higher values will increase the time it takes your test to run.                                                                                                                                                                                                        |

{% tabs %}
{% tab title="200: OK Sample response when using await strategy" %}
```json
{
    "data": {
        "runs": [
            {
                "result": {
                    "id": "l2AF-4096o2MpRLd5CrwX",
                    "source": "remote",
                    "browser": "firefox",
                    "browser_version": "120.0.1",
                    "operating_system": "linux",
                    "operating_system_version": "ubuntu",
                    "is_mobile": false,
                    "duration": 139824,
                    "started_at": 1707079870797,
                    "finished_at": 1707080010621,
                    "type": "suite",
                    "type_id": "9b391ad2-d2e7-4978-9e94-3173d50564d5",
                    "name": "Suite with data",
                    "status": "error",
                    "running_status": "completed",
                    "results": [
                        {
                            "id": "E4hjzqDAMnU5Pyk68tvB-",
                            "starting_url": "https://demoqa.com/automation-practice-form",
                            "source": "remote",
                            "browser": "firefox",
                            "browser_version": "120.0.1",
                            "operating_system": "linux",
                            "operating_system_version": "",
                            "is_mobile": false,
                            "duration": 29261,
                            "started_at": 1707079876249,
                            "finished_at": 1707079905510,
                            "status": "error",
                            "running_status": "completed",
                            "test_id": "9ae57564-b324-4734-9598-a52b987a2ad1",
                            "name": "demoqa tab to date",
                            "reason": "Element not found",
                            "summary": {
                                "total": 10,
                                "passed": 9,
                                "failed": 1,
                                "skipped": 0,
                                "ignored": 0
                            },
                            "test_runs": [
                                {
                                    "step_id": "lqe7kdnm1elzew3a4p9",
                                    "status": "success",
                                    "time_taken": 3436,
                                    "result_screenshot": {
                                        "imageDimensions": null,
                                        "imageData": ""
                                    },
                                    "title": "Setup: https://demoqa.com/automation-practice-form",
                                    "end_timestamp": 1707079879688,
                                    "start_timestamp": 1707079876252
                                },
                                {
                                    "step_id": "lqe7kkzg4c5fuhpan78",
                                    "status": "success",
                                    "time_taken": 818,
                                    "result_screenshot": {
                                        "imageDimensions": null,
                                        "imageData": ""
                                    },
                                    "title": "Scroll to element",
                                    "end_timestamp": 1707079880507,
                                    "start_timestamp": 1707079879689
                                },
                                {
                                    "step_id": "lqe7ku03wz26kaw7089",
                                    "status": "error",
                                    "time_taken": 16308,
                                    "result_screenshot": {
                                        "imageDimensions": null,
                                        "imageData": ""
                                    },
                                    "title": "Click 22",
                                    "error": "Element not found",
                                    "end_timestamp": 1707079905191,
                                    "start_timestamp": 1707079888883
                                }
                            ]
                        },
                        {
                            "id": "AxDq2BLKQHb4ecGhFBc9h",
                            "starting_url": "https://demoqa.com/",
                            "source": "remote",
                            "browser": "firefox",
                            "browser_version": "120.0.1",
                            "operating_system": "linux",
                            "operating_system_version": "",
                            "is_mobile": false,
                            "duration": 21898,
                            "started_at": 1707079914237,
                            "finished_at": 1707079936135,
                            "status": "success",
                            "running_status": "completed",
                            "test_id": "9aa0900e-d3f3-43e1-9696-acf1249640ba",
                            "name": "Demoqa with data",
                            "testData": {
                                "data_params": {
                                    "id": 1,
                                    "phone": "0909029394",
                                    "score": 18,
                                    "end_time": "2020-09-03T08:11:01.997Z",
                                    "lastname": "Sdk",
                                    "topic_id": null,
                                    "exam_type": null,
                                    "firstname": "Sodeeq",
                                    "created_at": "2020-09-03T08:05:14.501Z",
                                    "session_id": null,
                                    "start_time": "2020-09-03T08:05:14.497Z",
                                    "subject_id": 2,
                                    "updated_at": "2020-09-03T08:05:14.501Z",
                                    "completed_at": "2020-09-03T08:11:01.997Z",
                                    "total_questions": null,
                                    "recommended_topic": 346
                                },
                                "current_index": 0,
                                "total_loops": 3
                            },
                            "reason": null,
                            "summary": {
                                "total": 19,
                                "passed": 18,
                                "failed": 0,
                                "skipped": 1,
                                "ignored": 0
                            },
                            "test_runs": [
                                {
                                    "step_id": "lp19rhy2uv9ukjru41f",
                                    "status": "success",
                                    "time_taken": 4326,
                                    "result_screenshot": {
                                        "imageDimensions": null,
                                        "imageData": ""
                                    },
                                    "title": "Setup: https://demoqa.com/",
                                    "end_timestamp": 1707079918564,
                                    "start_timestamp": 1707079914238
                                },
                                {
                                    "step_id": "lp19rrxy2dxflca3uz4",
                                    "status": "success",
                                    "time_taken": 180,
                                    "result_screenshot": {
                                        "imageDimensions": null,
                                        "imageData": ""
                                    },
                                    "title": "Scroll to element",
                                    "end_timestamp": 1707079918745,
                                    "start_timestamp": 1707079918565
                                },
                                {
                                    "step_id": "lp19se046ajhe9gsu84",
                                    "status": "success",
                                    "time_taken": 1193,
                                    "result_screenshot": {
                                        "imageDimensions": null,
                                        "imageData": ""
                                    },
                                    "title": "Click \"Female\"",
                                    "end_timestamp": 1707079930187,
                                    "start_timestamp": 1707079928994
                                },
                                {
                                    "step_id": "lp19sqb1f56tpcovzbm",
                                    "status": "success",
                                    "time_taken": 1182,
                                    "result_screenshot": {
                                        "imageDimensions": null,
                                        "imageData": ""
                                    },
                                    "title": "Type \"Mobile Number\"",
                                    "end_timestamp": 1707079932563,
                                    "start_timestamp": 1707079931381
                                }
                            ]
                        },
                        {
                            "id": "yY1rCGEwj4jjgMPZPFqVr",
                            "starting_url": "https://demoqa.com/",
                            "source": "remote",
                            "browser": "firefox",
                            "browser_version": "120.0.1",
                            "operating_system": "linux",
                            "operating_system_version": "",
                            "is_mobile": false,
                            "duration": 20642,
                            "started_at": 1707079943804,
                            "finished_at": 1707079964446,
                            "status": "success",
                            "running_status": "completed",
                            "test_id": "9aa0900e-d3f3-43e1-9696-acf1249640ba",
                            "name": "Demoqa with data",
                            "testData": {
                                "data_params": {
                                    "id": 1,
                                    "phone": "982938394",
                                    "score": 18,
                                    "end_time": "2020-09-03T08:11:01.997Z",
                                    "lastname": "Sucrey",
                                    "topic_id": null,
                                    "exam_type": null,
                                    "firstname": "Bola",
                                    "created_at": "2020-09-03T08:05:14.501Z",
                                    "session_id": null,
                                    "start_time": "2020-09-03T08:05:14.497Z",
                                    "subject_id": 2,
                                    "updated_at": "2020-09-03T08:05:14.501Z",
                                    "completed_at": "2020-09-03T08:11:01.997Z",
                                    "total_questions": null,
                                    "recommended_topic": 346
                                },
                                "current_index": 2,
                                "total_loops": 3
                            },
                            "reason": null,
                            "summary": {
                                "total": 19,
                                "passed": 18,
                                "failed": 0,
                                "skipped": 1,
                                "ignored": 0
                            },
                            "test_runs": [
                                {
                                    "step_id": "lp19rhy2uv9ukjru41f",
                                    "status": "success",
                                    "time_taken": 3523,
                                    "result_screenshot": {
                                        "imageDimensions": null,
                                        "imageData": ""
                                    },
                                    "title": "Setup: https://demoqa.com/",
                                    "end_timestamp": 1707079947328,
                                    "start_timestamp": 1707079943805
                                },
                                {
                                    "step_id": "lp19stx6gbpvk619j8",
                                    "status": "success",
                                    "time_taken": 1148,
                                    "result_screenshot": {
                                        "imageDimensions": null,
                                        "imageData": ""
                                    },
                                    "title": "Click \"\"",
                                    "end_timestamp": 1707079964445,
                                    "start_timestamp": 1707079963297
                                },
                                {
                                    "step_id": "lp19t164dvpnu8rd3qt",
                                    "status": "skipped",
                                    "time_taken": 1,
                                    "result_screenshot": {
                                        "imageDimensions": null,
                                        "imageData": ""
                                    },
                                    "title": "Click \"English\"",
                                    "end_timestamp": 1707079964446,
                                    "start_timestamp": 1707079964445
                                }
                            ]
                        },
                        {
                            "id": "_FsdH9EERc4p6TiUTiF6F",
                            "starting_url": "https://demoqa.com/",
                            "source": "remote",
                            "browser": "firefox",
                            "browser_version": "120.0.1",
                            "operating_system": "linux",
                            "operating_system_version": "",
                            "is_mobile": false,
                            "duration": 23018,
                            "started_at": 1707079971297,
                            "finished_at": 1707079994315,
                            "status": "success",
                            "running_status": "completed",
                            "test_id": "9aa0900e-d3f3-43e1-9696-acf1249640ba",
                            "name": "Demoqa with data",
                            "testData": {
                                "data_params": {
                                    "id": 1,
                                    "phone": "0239383849",
                                    "score": 18,
                                    "end_time": "2020-09-03T08:11:01.997Z",
                                    "lastname": "Remi",
                                    "topic_id": null,
                                    "exam_type": null,
                                    "firstname": "Ola",
                                    "created_at": "2020-09-03T08:05:14.501Z",
                                    "session_id": null,
                                    "start_time": "2020-09-03T08:05:14.497Z",
                                    "subject_id": 2,
                                    "updated_at": "2020-09-03T08:05:14.501Z",
                                    "completed_at": "2020-09-03T08:11:01.997Z",
                                    "total_questions": null,
                                    "recommended_topic": 346
                                },
                                "current_index": 1,
                                "total_loops": 3
                            },
                            "reason": null,
                            "summary": {
                                "total": 19,
                                "passed": 18,
                                "failed": 0,
                                "skipped": 1,
                                "ignored": 0
                            },
                            "test_runs": [
                                {
                                    "step_id": "lp19rhy2uv9ukjru41f",
                                    "status": "success",
                                    "time_taken": 3199,
                                    "result_screenshot": {
                                        "imageDimensions": null,
                                        "imageData": ""
                                    },
                                    "title": "Setup: https://demoqa.com/",
                                    "end_timestamp": 1707079974497,
                                    "start_timestamp": 1707079971298
                                },
                                {
                                    "step_id": "lp19rrxy2dxflca3uz4",
                                    "status": "success",
                                    "time_taken": 181,
                                    "result_screenshot": {
                                        "imageDimensions": null,
                                        "imageData": ""
                                    },
                                    "title": "Scroll to element",
                                    "end_timestamp": 1707079974678,
                                    "start_timestamp": 1707079974497
                                },
                                {
                                    "step_id": "lp19t164dvpnu8rd3qt",
                                    "status": "skipped",
                                    "time_taken": 0,
                                    "result_screenshot": {
                                        "imageDimensions": null,
                                        "imageData": ""
                                    },
                                    "title": "Click \"English\"",
                                    "end_timestamp": 1707079994314,
                                    "start_timestamp": 1707079994314
                                }
                            ]
                        },
                        {
                            "id": "kpLTimp7IH22Z4bbnZ5C0",
                            "starting_url": "https://selectorshub.com/iframe-scenario/",
                            "source": "remote",
                            "browser": "firefox",
                            "browser_version": "120.0.1",
                            "operating_system": "linux",
                            "operating_system_version": "",
                            "is_mobile": false,
                            "duration": 6308,
                            "started_at": 1707080002322,
                            "finished_at": 1707080008630,
                            "status": "success",
                            "running_status": "completed",
                            "test_id": "9ac86c8a-1ba5-4e03-964a-0244568db13a",
                            "name": "3-level nested iframe",
                            "reason": null,
                            "summary": {
                                "total": 3,
                                "passed": 2,
                                "failed": 0,
                                "skipped": 1,
                                "ignored": 0
                            },
                            "test_runs": [
                                {
                                    "step_id": "lptkbls9dgilgw8zon",
                                    "status": "success",
                                    "time_taken": 4754,
                                    "result_screenshot": {
                                        "imageDimensions": null,
                                        "imageData": ""
                                    },
                                    "title": "Setup: https://selectorshub.com/iframe-scenario/",
                                    "end_timestamp": 1707080007077,
                                    "start_timestamp": 1707080002323
                                },
                                {
                                    "step_id": "lptkcjzvb51k6dt0f3j",
                                    "status": "skipped",
                                    "time_taken": 0,
                                    "result_screenshot": {
                                        "imageDimensions": null,
                                        "imageData": ""
                                    },
                                    "title": "Click Destiny",
                                    "end_timestamp": 1707080007077,
                                    "start_timestamp": 1707080007077
                                },
                                {
                                    "step_id": "lptkcozxl6pf6unin4",
                                    "status": "success",
                                    "time_taken": 1552,
                                    "result_screenshot": {
                                        "imageDimensions": null,
                                        "imageData": ""
                                    },
                                    "title": "Type \"Destiny\"",
                                    "end_timestamp": 1707080008629,
                                    "start_timestamp": 1707080007077
                                }
                            ]
                        }
                    ],
                    "summary": {
                        "total": 5,
                        "passed": 4,
                        "failed": 1
                    }
                }
            }
        ],
        "executions": [
            {
                "env": {
                    "id": "9933d94a-d119-4a24-9264-b8faaf9eb807",
                    "name": "Desktop mini",
                    "width": 1024,
                    "height": 650,
                    "browser": "firefox",
                    "operating_system": "linux",
                    "project_id": "98a22a29-78c2-4f46-bc02-82d391cab0ab",
                    "created_at": "2023-05-19T08:01:19.000000Z",
                    "updated_at": "2023-05-19T08:01:19.000000Z"
                },
                "execution_id": "l2AF-4096o2MpRLd5CrwX"
            }
        ]
    },
    "message": "Suite run completed"
}
```
{% endtab %}
{% endtabs %}

### Sample request using cURL

```url
curl --location 'https://scr.getscandium.com/suites/execute' \
--header 'Accept: application/json' \
--header 'x-api-token: <API TOKEN>' \
--header 'Content-Type: application/json' \
--data '{
    "project_id": "<PROJECT ID>",
    "suite_id": "<SUITE ID>",
    "strategy": "await"
}'
```

