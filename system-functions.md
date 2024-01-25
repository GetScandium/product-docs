---
description: Generate and use dynamic values in your tests
---

# System Functions

Systems functions are very similar to [variables](variables.md), but functions are built-in variables that come with Scandium.

Functions help you generate dynamic and unique values in your tests.

Let's take a quick look at the available functions on Scandium:

**Email**: To help you generate unique emails. Useful in cases where you need to test signup flows and you need a unique email each time the test runs. e.g _itKRJ.lkdhuz1bql@testmail.getscandium.com_

**Num**: To help you generate numbers of any length. e.g _19660200324_

**Range**: To help generate a number within two boundaries. e.g _236_

**Alpha**: To generate letters of the alphabet. You can specify the number of letters needed and even which character set you want the letters to come from. e.g _itKRJ_

**Alphanum**: Similar to alpha, but also includes numbers in the generated value. e.g _JlU1ZZcr_

**Date**: To generate date value in a desired format. e.g _15/09/2023_

**Time**: Generate timestamp value (epoch time). e.g _1694463242839_

**Datetime**: To generate datetime value e.g _Mon Sep 11 2023 21:13:50 GMT+0100 (West Africa Standard Time)_

#### Using a system function

You can insert a function anywhere you can insert a variable. To use a function in the value of a text field, expand the settings of the step where you want to insert the function, then click on the "Insert function" button, and choose the desired function to insert.

<figure><img src=".gitbook/assets/image (8).png" alt=""><figcaption><p>Click on insert function button</p></figcaption></figure>

<figure><img src=".gitbook/assets/image (9).png" alt=""><figcaption><p>Select the function to insert</p></figcaption></figure>

<figure><img src=".gitbook/assets/image (10).png" alt=""><figcaption><p>Function inserted</p></figcaption></figure>

Once you select a function to insert, its notation will be added in the Text to Assign field `{{num(11)}}` . When the test is running and it gets to this step, the notation will be replaced with a randomly generated 11-digit number.

