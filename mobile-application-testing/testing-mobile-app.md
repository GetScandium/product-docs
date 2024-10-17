---
description: Record your test case in a mobile emulator within your browser
---

# Testing mobile app

Once you have set up a mobile project and obtained the app bundle for testing ([Check here for how to obtain a test-compatible bundle for your application](uploading-apps/)), the next step is to upload the app into your project.

### How to upload app

Within your mobile project

1.  Click on the Apps menu\


    <figure><img src="../.gitbook/assets/image (68).png" alt=""><figcaption><p>Click on Apps menu</p></figcaption></figure>

    This should take you to the apps listing page
2.  Click on the "Upload new app" button\


    <figure><img src="../.gitbook/assets/image (69).png" alt=""><figcaption><p>Upload new app</p></figcaption></figure>

    This reveals a modal where you can choose your app bundle located on your computer. The modal contains instructions for obtaining both iOS and Android app bundles for testing
3. Once file is selected, click on the SAVE button to upload application. This might take a while depending on the size of the file. \
   **NOTE: There is a soft limit of 150MB file size. i.e if  you upload an app greater than this size, it might not get uploaded.**
4.  When your upload is successful, you will find the app listed on the same page\


    <figure><img src="../.gitbook/assets/image (70).png" alt=""><figcaption><p>App listing showing app name, bundle ID and platform</p></figcaption></figure>

    You can upload multiple apps into a project,  and you can also choose to create a different project for each app.

### Create a new test

With your app uploaded, on the apps listing page, click on your application.

This takes you to the app details page. This page shows you the details of the application such as its name, version code, version name, the author, the platform date it was uploaded and the list of test cases created for the application.

You can add a new test case by clicking on the 'New Test' button

<figure><img src="../.gitbook/assets/image (71).png" alt=""><figcaption><p>Click on new test</p></figcaption></figure>

### Recording a test

On the test creation page, an emulator is loaded alongside a toolbar for additional functions

<figure><img src="../.gitbook/assets/image (72).png" alt=""><figcaption><p>Emulator and options</p></figcaption></figure>

The emulator/simulator displayed will be based on the type of application uploaded. An android emulator will be displayed for android applications, while an iOS simulator will be displayed for iOS apps.

To begin creating your test, click on the `Record` button.

After clicking on the Record button, the app gets installed into the emulator, once installation is complete, recording starts. You can now begin to carry out all the necessary steps needed for your test case.

**NB: Everytime you record/run your test, the application will get installed into the device afresh, so you're guaranteed that your testing starts from a clean slate.**

Once you are done recording all your steps, click on the 'End Session' button.

Scroll to the bottom of the page to view all steps recorded for your test. You can inspect the recorded steps to be sure it captures all you need.

Save your test by clicking on the SAVE button. This will prompt you to provide a name for the test case.

<figure><img src="../.gitbook/assets/image (74).png" alt=""><figcaption><p>Enter a name for your test</p></figcaption></figure>

Enter a name for your test case, and an optional description. You can leave the default step timeout and prestep delay. Then save your changes by clicking on the Save button.

**Run the test recorded by clicking on the 'Run/Replay' button**

<figure><img src="../.gitbook/assets/image (73).png" alt=""><figcaption><p>Run your test</p></figcaption></figure>

