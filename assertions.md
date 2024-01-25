---
description: Validate the correctness of an outcome
---

# Assertions

What is a test without an assertion?

Assertions are how we verify that the execution of a step gives an expected outcome. For example, if we are creating a test to test that a user can not log in with an incorrect username and password combination, we will assert that an error message _incorrect username/password_ is displayed after clicking on the login button.

### How to assert with Scandium

By clicking on the green checkmark (✅) on the Scandium toolbar, the assertion panel is displayed.

<figure><img src=".gitbook/assets/image (43).png" alt=""><figcaption></figcaption></figure>

There are two broad categories of assertions you can make:

1. Against the page itself
2. Against an element on the page

#### Against the page

You can assert the value of the page title, the page url, or that the page contains a certain text.

<figure><img src=".gitbook/assets/image (44).png" alt=""><figcaption></figcaption></figure>

#### Assert against an element on the page

You can also select any element on the page to assert against. When you opt to assert against an element on the page, the page is put into inspection mode such that any element you hover your mouse on is highlighted. You can click on any element to assert against it.

To assert against an element, on the assertions panel window, click on the big blue button:

<figure><img src=".gitbook/assets/image.png" alt=""><figcaption><p>Activate assertion for element on a page</p></figcaption></figure>

Once the button is clicked on, the page is put into inspection mode, you can hover your mouse on any element on the page. You should see the element highlighted with a dotted border around it.

<figure><img src=".gitbook/assets/image (1).png" alt=""><figcaption><p>Inspecting an element to be asserted against</p></figcaption></figure>

Click on the element you want to assert against. Then back on the assertion panel, from the list of commands, choose your desired assertion from the dropdown.

<figure><img src=".gitbook/assets/image (2).png" alt=""><figcaption><p>Choose desired element assertion</p></figcaption></figure>

Currently, you can make the following element assertions:

| Assertion type                  | Description                                                                                                                      | Extra                                                                              |
| ------------------------------- | -------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------- |
| Element should be visible       | Verify that the target element is visible on the page                                                                            | Applies to all elements                                                            |
| Element should not be visible   | Verify that the target element is not visible on the page                                                                        | Applies to all elements                                                            |
| Element should contain text     | Verify that the target element **contains** the specified string.                                                                | Applies to all elements that can have text                                         |
| Element should not contain text | Verify that the target element does not contain the specified string                                                             | Applies to all elements that can have text                                         |
| Element should be enabled 🆕    | Verify that the target element is enabled. The element must be visible, and must not have the `readonly` or `disabled` property. | Applies to elements that can have the disabled property                            |
| Element should be disabled🆕    | Verify that the target element is disabled. The assertion fails if the element is found to be enabled.                           | Applies to elements that can have the disabled property                            |
| Element has HTML property 🆕    | Verify that the target element has a given property name and a corresponding matching value.                                     | Applies to all elements                                                            |
| Element has CSS property 🆕     | Verify that the target element has a given CSS attribute name and a corresponding matching value.                                | Applies to all elements                                                            |
| Checkbox should be checked      | Verify that the target checkbox element is checked                                                                               | Applicable when the selected target element is either a checkbox or a radio button |
| Checkbox should not be checked  | Verify that the target checkbox element is not checked                                                                           | Applicable when the selected target element is either a checkbox or a radio button |

#### Updating an assertion

If you added assertions during the recording of your test case, you can update the assertion type or expected value of the assertion from the step settings on your test editor.

![](<.gitbook/assets/image (45).png>)
