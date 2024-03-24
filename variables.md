---
description: Creating and using dynamic values in your tests
---

# Variables

### Creating variables

A variable is a value store, whose value can change depending on certain conditions. On Scandium, there are several ways by which you can create a variable, and we will look at each of these methods.

**Step Variables**

You can assign the _value_ or _text content_ of a step's target element to a variable. When you assign a `input` type step to a variable, whatever value is entered into the input field will be extracted and stored in the variable. For other step types like `click` , the text content of the step target element will be extracted and assigned to the variable. A variable created from a step can be used (i.e referenced) in subsequent input steps or in assertion values.

To create a step variable (i.e assign a step to a variable), in the settings of a step, click on the "Assign to variable" button.

<figure><img src=".gitbook/assets/image (14) (1).png" alt=""><figcaption><p>Click on assign to variable button</p></figcaption></figure>

You will then be prompted to enter a name for the variable. This name is what you will use to reference the variable as we will soon see.

When choosing a name for your variable, ensure you choose a name that is easy to read, unique and contains only alphanumeric characters.

<figure><img src=".gitbook/assets/image (15) (1).png" alt=""><figcaption><p>Give a name to your variable</p></figcaption></figure>

Once you enter a name for your variable and save, you will see the variable name now reflecting in the settings panel.

<figure><img src=".gitbook/assets/image (17) (1).png" alt=""><figcaption></figcaption></figure>

With the above steps, we have created a step variable, we will see shortly how to make use of the variable which we have created.

#### Test Variables

Test variables are variables created at the test level. They are available to all steps within the test case in which they have been defined. They help you define a value once, and reuse this value in any step within the test.

Differences between a step variable and a test variable

| Test Variable                            | Step Variable                                                                                     |
| ---------------------------------------- | ------------------------------------------------------------------------------------------------- |
| Can be used in all steps within the test | Can only be used in steps that come after the assigning step                                      |
| It's value can be known beforehand       | It's value is not known before rather. Rather, it's value is extracted from the element of a step |

To create a test variable, click on the test settings icon

<figure><img src=".gitbook/assets/image (18) (1).png" alt=""><figcaption></figcaption></figure>

Then click on the "Test case variable" tab

<figure><img src=".gitbook/assets/image (19) (1).png" alt=""><figcaption></figcaption></figure>

You can then click on the "Add new variable" to add a new variable. This will provide you with two new fields to enter the variable name and its value.

<figure><img src=".gitbook/assets/image (21).png" alt=""><figcaption></figcaption></figure>

You can add as many variables as you need, once all has been added, click on the "Save" button. All of the added variables will now be available for you to use in your test steps.



### Using Variables

Variables can be _used_ in steps that require an input value. This includes steps that of text fields, and assertions that require additional text.

To insert a variable into the value of a text, expand the settings panel of an input step, then below the "Text to assign" field, locate the "Insert variable" button and click on it.

<figure><img src=".gitbook/assets/image (23).png" alt=""><figcaption><p>Click on insert variable</p></figcaption></figure>

A modal will come up, from there, you will see a list of all variables available to you for insertion. Each item on the list will also show you information about how the variable was created e.g Test case, step, file, global etc.

<figure><img src=".gitbook/assets/image (24).png" alt=""><figcaption><p>Select variable to insert</p></figcaption></figure>

Once a variable is selected, it will then be inserted into the text to assign field.

<figure><img src=".gitbook/assets/image (25).png" alt=""><figcaption><p>A variable inserted.</p></figcaption></figure>

As you can see, it is wrapped in two curly brackets `{{ }}` . The name of the variable is contained within the brackets, prefixed by the source of the variable e.g _test._ denoting that it's a test case variable, _step._ denoting that it's a step variable, and so on.
