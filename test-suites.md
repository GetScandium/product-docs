---
description: Organize your tests in Suites
---

# Test Suites

A test suite is a collection of test cases that often share similar rules and configurations.

After you have created your test cases, you ideally don't want to run them one by one. Instead, you want to run multiple test cases at a time.

Let's look at a few situations where you might want to run a test suite instead of a single test case:

1. You want to run certain critical test cases in your deployment pipeline during deployment.
2. You want to run certain test cases at a scheduled frequency.&#x20;
3. You want to run all test cases related to a particular module or feature.
4. You want to manually run all or many test cases within a project.

The above situations and more can necessitate the need for test suites. You can create different suites for different purposes.

Scandium allows you to create and manage test suites easily.

#### Creating a test suite

Click on the "Suites" menu to go to the test suites page

<figure><img src=".gitbook/assets/image (35).png" alt=""><figcaption><p>Suites menu</p></figcaption></figure>

Then click on "New suite" to create a new suite

<figure><img src=".gitbook/assets/image (36).png" alt=""><figcaption><p>Click on new suite button</p></figcaption></figure>

Give the suite a **name and description** to identify it.&#x20;

**Then add the execution environments** where you want this suite to be executed. By adding multiple exec. environments, you are able to achieve cross-browser testing. Anytime you run the suite, Scandium will run the tests in the suite on the different environments you added.

**Select if you want the tests in the suite to run in sequence or in parallel**. Sequential mode will run the tests one after the other, while parallel mode will run multiple tests at the same time. In parallel mode, the order of execution is not guaranteed, so if your tests depend on one another, better to run them in sequence. Scandium will run them in the order they were arranged in the suite.

**Add starting url** to the suite. This is optional. If you want to override the starting URL for all tests within the suite, you can provide a URL here. When the suite runs, it will replace the starting URLs of the individual tests with the URL you specified here.

**Add** **tests** to the suite. You can then select one or more tests to add to the suite.

<figure><img src=".gitbook/assets/image (38).png" alt=""><figcaption><p>Add tests to suite</p></figcaption></figure>

#### How to run a test suite

To trigger a test suite to run manually, click on the kebab menu of the test suite on the suites page.

<figure><img src=".gitbook/assets/image (39).png" alt=""><figcaption></figcaption></figure>

PS: At this time of this writing, you can only trigger your test suites to run locally.
