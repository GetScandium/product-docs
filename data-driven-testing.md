---
description: Run the same test with different data
---

# Data-driven Testing

Data-driven testing is a software testing technique that separates test data from test scripts. It enables testers to reuse test scripts for different sets of data. Scandium provides built-in features to help you run various test data in just one test case by importing your test case in either Excel, CSV, or JSON format into Scandium.&#x20;

When a data source is added to a test case, running the test case will run for each row in the datasets of the uploaded spreadsheet.

### How to import a data source to a test case on Scandium

1. Record your initial test scenario as usual
2. Create a spreadsheet containing your data set from any Office suite software. Ensure the first row of your data set contains the column header names. These columns will be referred to as corresponding variables within your test. Save and download the file on your computer.
3.  On Scandium, click the Settings Icon ⚙️ on the test case page.\


    <figure><img src="https://lh7-us.googleusercontent.com/m2Zzy93hyl-n9h9uw9gV5MSRmD0vE3xFVui3soJZBYRjtv8_xmC9fYuYEITl9MdI2hw-55FGkprpYQNRuCP9NREkethb384TnkpbnqC1oL5QsIH8P3LCzLN9UnCOJWIHN614EWsA0J0PQGAamGPdj3s" alt=""><figcaption></figcaption></figure>


4.  Click the "Upload File" button and select the file you want to upload (created from step 2)



    \


    <figure><img src="https://lh7-us.googleusercontent.com/bX0D1COIc6KuGKE2Q6c1vVeacJTVrzbYQ0c_lSkX3og7o1qzndLQFW5jTtpon66pCa7dZ_simSnHoDaQx01JPZ5G_wOtHxZ3OniVCQav8mpd-w_MhZDXcdHUIN3lrKaMEgoiOkTlnSmtZc_yrnjmCOA" alt=""><figcaption></figcaption></figure>


5.  Once the file has been read, its content will be displayed in JSON format in the text editor below the button. Click on the Save button to save your changes.\


    <figure><img src="https://lh7-us.googleusercontent.com/6cMbuI5bwae1MtM2NAUQ1nitM80MhipytS9cEm1AFOaUr1Ny_Lhjc-HeUnTv3sS_OZN4KwnowXnuYcv20yHCtpoDG0yWR1dt79IOMVbZducAnkXTXzoAw-Vt3tLPocdf--fXWTQeX5nNZJDqKrU1_Kg" alt=""><figcaption></figcaption></figure>
6.  Click on the Back arrow to go back to the list of steps\


    <figure><img src=".gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>



### Using imported data as variables within steps

Now that a data source is imported and attached to a test case, you need to update the steps in which you desire the columns from the data source to be used.

On the test step of where you want the data imported to reflect, click the ⊕ button, the click settings icon ⚙️ of the step

<figure><img src="https://lh7-us.googleusercontent.com/XeGtOWhLZKPUieNyT_Ml19wFNhlS_RfxyFCIWdv8MLov6zrRsbGb7QjeG4KrcGIA3Tq6sOChWgq2yXDO_gs2ol__HbwIMCEdjEQkeL94Hy2jVr1GtOQnM1T1oKo0YBAVP-ZHIsp4Eey3i0S-YT4zPqE" alt=""><figcaption></figcaption></figure>

In the “text to assign” text bar, delete the existing text data

<figure><img src="https://lh7-us.googleusercontent.com/vFQjjAtg12q3aNbezxrQC8EoJSnvKlUmpJR7iTEZPk96aalTWoxVynSd9ru84FLidx9I1WI6Wc2CdDuu5NZLheD5i85FMHMcm8QO6uCu2pSCEjHGWo1bbLermY1n7DbKDW1rqeTP8UFdLa10Cf8Z_TA" alt=""><figcaption></figcaption></figure>

Click on the "Insert Variable" button

<figure><img src="https://lh7-us.googleusercontent.com/H2TJUIcixau-ogymm8VykJqBOFpuoZtJIeek_IEyC01XLQ4mEf6b5p9a2SGYhgHPMskWw3Gji4Vp4Rw7pS11J7GL-HopAhn6P3q_5ixoDO8jmsDvIFT-b0YIX9L_pCbFVBW5RVtZUpQuBbt5X3av7Eg" alt=""><figcaption></figcaption></figure>

In the ensuing modal that displays the list of variables you can select, you should see that each header in the spreadsheet you uploaded has now been mapped to a variable name, with an indicator that shows that the variable is from an external file (the data source). Select the appropriate column from the list.

Repeat this for all steps that need input from the data source.

<figure><img src="https://lh7-us.googleusercontent.com/ALXu0xIyIhnW9uKv42kEOTZ823fieU0xdjITMFxRvqjlB4XHhF-TeDFmqCxOniKsiRZtGnQXklN0UF_LXvHpI21XpV9GmLq0E51-BfBNqJ9JbV_VD6vYO56CEDQdJxaNDit2D4b4xPVvXzQmug8IYHg" alt=""><figcaption></figcaption></figure>

Upon selection, the selected variable will be inserted into the "Text To Assign" field of the step

<figure><img src="https://lh7-us.googleusercontent.com/kIApdf-Yonv8zcK1AaTO4NKBWfhmjxRByIh9izv6NvTVeIGuQGFoHxjzunxn6CDsS8KcVk5uf-9ddxaagZAhAPfO4isA0iZm9ccVANBi5w4w2gydWy7CxO1L30v49MlMN-E8WjY-JhbOfoDBbnLTrVM" alt=""><figcaption></figcaption></figure>

You can now save and run your test.

> Note: Data driven testing will trigger multiple test runs for the same test, so be aware of the usage required before using.
>
> For example, if your spreadsheet contains 101 rows (including the headers), the test will run 100 times anytime you run it.

{% hint style="info" %}
On the local runner, Scandium will only run the test for the first 10 rows
{% endhint %}

You can view the result of a data-driven test run by visiting the **Suites Results** menu.
