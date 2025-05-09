---
description: Get started with Scandium's standalone API testing module
---

# Getting Started

### Create a basic API request

<figure><img src="../.gitbook/assets/image (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

On the Scandium API runner interface, you are able to create a new API request. To create an API request, you need to select the method of the request and provide the API URL (endpoint).

Press the Send button to initiate the request or press the Save button to save the request.

You can change the name/title of the request before and after saving:

<figure><img src="../.gitbook/assets/image (2) (1) (1).png" alt=""><figcaption></figcaption></figure>

Enter the desired name for your test case and press the Save button.

#### Try an example request

Method Type: GET

API URL: [https://api.edudream.fr/location/country](https://api.edudream.fr/location/country)

<figure><img src="../.gitbook/assets/image (3) (1) (1).png" alt=""><figcaption><p>An API request with sample response</p></figcaption></figure>

#### Additional information on API requests

The Scandium API runner interface allows you to add additional information to your API requests where needed.

**Query parameters:** Can be added from the 'Params' tab

<figure><img src="../.gitbook/assets/image (4) (1) (1).png" alt=""><figcaption></figcaption></figure>

**Authorization:** Scandium supports multiple authorization types out of the box, including Bearer Token, Basic Auth, API Key, Digest Auth, Oauth 1.0

<figure><img src="../.gitbook/assets/image (5) (1).png" alt=""><figcaption></figcaption></figure>

**Headers:** You can add several header key-values as required by your API

<figure><img src="../.gitbook/assets/image (6) (1).png" alt=""><figcaption></figcaption></figure>

**Body:** Scandium supports multiple body types as payload for your request. This includes: form-data, x-www-form-urlencoded, JSON, XML, Text, HTML and GraphQL.

<figure><img src="../.gitbook/assets/image (7) (1).png" alt=""><figcaption></figcaption></figure>

### Adding assertions to API requests

When you make API requests, you want to validate that the request outcome meets your expectations. With Scandium API Runner, you can add assertions to your API tests. To add. these assertions, click on the 'Assertions' tab.

You can add assertions for the following:

* Status code
* Response header
* Response body type
* Response body content
* Request duration

<figure><img src="../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

To add an assertion,&#x20;

1. Select the assertion type.
2. Select a condition for the assertion.
3. Input the value to be checked for.

<figure><img src="../.gitbook/assets/image (9).png" alt=""><figcaption><p>Select assertion operator/condition</p></figcaption></figure>

<figure><img src="../.gitbook/assets/image (10).png" alt=""><figcaption><p>Enter assertion value to check for</p></figcaption></figure>

You can also combine multiple assertions for one request.

### Viewing API Response

After sending your API requests, you can see the response to your requests in the tab below the request area.

This tab shows you the status code, the duration of the request, the size of the response and the content of the response. You can view the body of the response in JSON, look at the headers and also inspect the Assertions Result tab for result of the assertions you added.

<figure><img src="../.gitbook/assets/image (11).png" alt=""><figcaption><p>Response body</p></figcaption></figure>

<figure><img src="../.gitbook/assets/image (12).png" alt=""><figcaption><p>Assertion result</p></figcaption></figure>

### Variables in requests

Variables make it easy to reuse a value in multiple API tests. For example, imagine the APIs you are testing have the base url `https://example.com/api`. This part of the URL is common to all endpoints, such that a login endpoint would like `https://example.com/api/login` while a registration endpoint would like `https://example.com/api/register`.

Now imagine you want to test these APIs across different environments such as staging, test and production, where all these environments have different base URLs. Normally, you'd have to update all test cases with the specific environment URL each time you want to run your API test against such environment.

But if you create the base URL as a variable, you'd only have to make the change once.

#### How to create a variable

You can create a variable by clicking on the Variable submenu

<figure><img src="../.gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>

From the modal that appears, you can then add the names and values for your variables. You can add as many variables as you need.

<figure><img src="../.gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>

Click on the Save button to save your newly added variable.

#### Using a variable (How to make reference to a variable)

Once you have created a variable, it will be available for you to use within your tests. Variables can be used in the endpoint field, headers, parameters and body of the request.

To reference a variable, type `{{` (two curly braces), this will bring up a suggestion of the list of variables available, you can then select one from the list.

<figure><img src="../.gitbook/assets/image (16).png" alt=""><figcaption><p>Choose a variable from the suggestion</p></figcaption></figure>

<figure><img src="../.gitbook/assets/image (17).png" alt=""><figcaption><p>Variable plus other string</p></figcaption></figure>

When  the request is sent,  the variable (denoted by `{{base_url}}`) will get replaced by its value which in this case is [`https://api.edudream.fr`](https://api.edudream.fr)&#x20;

### Dynamic values and functions in requests

When sending an API request, there could often be situations where you need to send a randomized value to your endpoint. For example, when testing a registration endpoint, you want to have a different email address value sent every time the request is made so that your application doesn't give you a "<mark style="color:red;">email already exists</mark>" error. This could also apply  to phone numbers, usernames etc.

Scandium makes it easy for you to achieve this dynamic data input. Similar to the variables in requests, dynamic functions also use the `{{ }}` notation.

You can use this dynamic values in your:

* URL
* Query parameter keys and values
* Header keys and values
* Body payload
* Cookies keys and values

To use the dynamic value in an accepted field, type the `{{` where the value is required

<figure><img src="../.gitbook/assets/image.png" alt=""><figcaption><p>Type two opening curly braces</p></figcaption></figure>

A suggestion popup opens up from which you can then click on the 'Dynamic Values' button. Clicking on the button above shows you a modal containing multiple available functions you can choose from.

Below are the functions you can choose from:

**Email**: To help you generate unique emails. Useful in cases where you need to test signup flows and you need a unique email each time the test runs. e.g _itKRJ.lkdhuz1bql@testmail.getscandium.com_

**Num**: To help you generate numbers of any length. e.g _19660200324_

**Range**: To help generate a number within two boundaries. e.g _236_

**Alpha**: To generate letters of the alphabet. You can specify the number of letters needed and even which character set you want the letters to come from. e.g _itKRJ_

**Alphanum**: Similar to alpha, but also includes numbers in the generated value. e.g _JlU1ZZcr_

**Date**: To generate date value in a desired format. e.g _15/09/2023_

**Time**: Generate timestamp value (epoch time). e.g _1694463242839_

**Datetime**: To generate datetime value e.g _Mon Sep 11 2023 21:13:50 GMT+0100 (West Africa Standard Time)_

**Boolean**_:_ To generate one of _true_ or _false_.

<figure><img src="../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

**NB**: In JSON payload, you should still insert the dynamic function inside quotes

<figure><img src="../.gitbook/assets/image (3).png" alt=""><figcaption><p>Put dynamic functions in quote</p></figcaption></figure>
