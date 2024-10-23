---
description: >-
  Test workflows that involve validating that emails are sent, or extracting
  content from emails sent.
---

# Email Testing

{% hint style="info" %}
As of November 12, 2023, Email Testing is a free feature on Scandium
{% endhint %}

When testing applications, it is common for emails to be triggered by certain actions. E.g When completing your order on an e-commerce website, an email can be sent to you showing the order confirmation.

You may want to access your email to confirm that an email was indeed sent to the user, or perhaps click on a link in the email, or even extract a value from the email to be used in later steps within the test.

Instead of having to access a 3rd party mail provider during your tests, Scandium has an inbuilt email service that can be used to access emails triggered during your tests.

### Scandium MailBox Service

We provision an email inbox for you that is available to you per project i.e each project has its own inbox. In order to receive emails to the inbox of a project, send your emails to an address in the structure `<anything>.<uniqueid>@testmail.getscandium.com` where \<anything> is a prefix could be any random string, the most important part of the email is the `.<uniqueid>@getscandium.com`

A real example would be `wJQvB.jeiuigghep@testmail.getscandium.com` where `wJQvB` could be any string (prefix), `jeiuigghep` is the project unique mail ID.  Now, regardless of what the prefix is, any email sent to the address that matches \*.jeiuigghep@testmail.getscandium.com will be received in the same inbox.

Essentially, emails sent to `sdk.jeiuigghep@testmail.getscandium.com` and `testing123.jeiuigghep@testmail.getscandium.com` will be received in the same inbox.

An easy way to get the email pattern for your project is to visit the test creation page, then click on the Mail icon

<figure><img src=".gitbook/assets/image (3) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

Once you click on the mail icon, then click on the 'copy' icon in the popup revealed.

<figure><img src=".gitbook/assets/image (5) (1) (1).png" alt=""><figcaption></figcaption></figure>

The copied email can then be used wherever you need to receive email in your app. For example, it can be used in registration forms that need email.

If your registration form triggers an email e.g an activation email, Scandium will receive this email for you in the provided inbox. You can access this inbox anytime by clicking on the "Visit mailbox" link as shown in the image above.

### Accessing Emails During Test Recording

When recording your test case, after performing an action that is supposed to trigger an email reception, click on the Mail Icon on the Scandium Toolbar in your recording window.

<figure><img src=".gitbook/assets/image (6) (1) (1).png" alt=""><figcaption><p>Mail icon on scandium toolbar</p></figcaption></figure>

This will open up your mailbox. All the emails directed to your project email structure will be found in this mailbox and you can interact with it like any other web page. You can make assertions, do clicks and so on.

<figure><img src=".gitbook/assets/image (7) (1) (1).png" alt=""><figcaption><p>Scandium email inbox</p></figcaption></figure>

### Generating Dynamic Emails

A common scenario during testing is testing registration flows where you are required to use a new/unique email for every new registration. Scandium makes this a breeze. By combining the project mail service provisioned for you and the [Systems Functions](system-functions.md), you can generate a dynamic and randomized email during every run. We will look at an example below.

We have an inbuilt \{{time(0)\}} function that generates a unix time based on the current time. By using this as the prefix of your Scandium project mail, you get a dynamic email each time (since the time of run will always be different). `{{time(0)}}.lkdhuz1bql@testmail.getscandium.com`



#### Steps to using Dynamic Email in a test step

1. Go to the step that needs the dynamic email value
2. Expand the step and click on its settings icon to open its settings sidebar
3. Click on the "Insert Function" below the "Text To Assign" field of the step
4. Select "Email" from the list of functions
5. In the "offset" field, enter 0 or any other number
6. Click on "Insert". This will replace the value in the "Text to Assign" field to something like `{{time(0)}}.lkdhuz1bql@testmail.getscandium.com`
7. Whenever you re-run this step, you will see the email generated looks like `1699823938.lkdhuz1bql@testmail.getscandium.com`. The \{{time\}} function gets replaced with the actual time value.

This is how you achieve dynamic email.

