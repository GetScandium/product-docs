---
description: You can use Scandium to monitor your API endpoints
---

# Scheduling and Monitoring

Scheduled API tests are tests that run at predefined times and intervals. For instance, you want to know at every hour if your APIs still work as expected.

To schedule API runs with Scandium, you need to [create an API suite](api-suites.md#create-a-new-test-suite). An API suite is a collection of multiple  API tests. When you run this single suite, all test cases contained within the suite will run.

{% hint style="info" %}
To get the best out of your API tests, you should add [assertions](./#adding-assertions-to-api-requests) to each test case.
{% endhint %}

### How to schedule an API suite

To schedule an API suite, open the test suite you want to schedule by click on its name from the list of API suites you have created.

Click on the 'Schedule' button

<figure><img src="../.gitbook/assets/image (66).png" alt=""><figcaption></figcaption></figure>

From the ensuing modal, provide a name and description for the schedule, then set the frequency for which you want the suite to be run.

You can choose from the options hourly, daily, or specific days of the week.

<figure><img src="../.gitbook/assets/image (67).png" alt=""><figcaption></figcaption></figure>

Then click on the 'Save' button.
