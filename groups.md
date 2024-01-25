---
description: Create reusable steps by combining multiple steps into one
---

# Groups

When you create multiple test cases, you start to notice that there are steps that occur in the same sequence across these multiple test cases. For example, if many of your application features are behind a login wall, for every test you create, the login steps are essential.

#### Why create groups?

* Grouped steps on Scandium make "reuse" very easy.
* You can apply a common operation to the group containing the steps.
* Apply an edit once to a group and have it take effect in all tests using the group.

#### How to create a group

1. Open anyone of your test cases containing the steps you want to turn into a group.
2.  Select all the steps you want to combine by _checking_ the checkbox on the step.\


    <figure><img src=".gitbook/assets/image (46).png" alt=""><figcaption></figcaption></figure>
3. Click on the kebab menu above the steps to reveal an additional options dropdown.
4.  From the list, select "Add to group"\


    <figure><img src=".gitbook/assets/image (47).png" alt=""><figcaption></figcaption></figure>


5. In the opened modal, fill in a title and description for the group, also set if you want the group to be reusable (default). Reusable groups will be available in other tests.
6. Finally, click on the "Create Group" button. The selected steps will now be combined into one.

<figure><img src=".gitbook/assets/image (48).png" alt=""><figcaption></figcaption></figure>

#### Viewing the steps in a group

You can now see the group in the list of steps within the test case. The group is indicated with a _folder_ icon, also showing the number of steps within the group.

<figure><img src=".gitbook/assets/image (49).png" alt=""><figcaption></figcaption></figure>

To view the individual steps within the group, click on the _blue plus_ button (➕)

Then click on the _eye icon,_ this will expand the group, showing the steps inside it.

<figure><img src=".gitbook/assets/image (50).png" alt=""><figcaption></figcaption></figure>

#### Editing a group

Within a test, you can edit the settings of a group just like you would do any other single step.

[See settings you can do on a step](step-settings.md)

#### Duplicating a group

In addition to individual step settings on a group, you can also clone a group by using the _Replace with duplicate_ settings option.

<figure><img src=".gitbook/assets/image (51).png" alt=""><figcaption></figcaption></figure>

Here's why you may need to replace a group with a duplicate:

In a test, when you edit a reusable group (e.g set a precondition, or change its pre-step delay) that is used in multiple tests, these changes apply across all tests using the group. If you however don't intend for this, but instead, you want the group update to only apply to the current test you are editing, you can replace the group with a duplicate. This will create an exact copy of the group, that will now no longer be cross-updated. You can update the group as you desire, and this change will not propagate to other test cases.

<figure><img src=".gitbook/assets/image (52).png" alt=""><figcaption></figcaption></figure>

#### Inserting an existing group into a test

Now that you have a reusable group, you can insert the group into any test you desire.

To do that:

1. Open the test where you want to insert your group
2. _Check_ the checkbox of the step occupying the position where you want the group inserted
3. Click on the kebab icon above the steps
4. From the dropdown, select "Insert group Before".
5. From the list of groups displayed, select the group you want to insert.
6. Voila!

#### Renaming a group

To rename a group:

1. Open any test that uses the group
2. Open the settings of the group step. (➕) => ⚙️
3.  In the title field, insert the new desired name for the group\


    <figure><img src=".gitbook/assets/image (54).png" alt=""><figcaption><p>Update group name</p></figcaption></figure>

#### Deleting/Removing a group from a test

To remove a group from within any test using the group,

1. Open the test you want to remove the group from
2. Open the settings of the group step. (➕) => ⚙️
3.  At the bottom of the settings panel, click on the DELETE button\


    <figure><img src=".gitbook/assets/image (53).png" alt=""><figcaption><p>Delete a group from a test</p></figcaption></figure>



#### Adding new steps to an existing group

After you have initially created your group with some steps, you might need to later add additional steps to the group. To achieve this:

1. Open the test containing the step(s) you want to add to an existing group
2. _Check_ the checkbox on the step(s).
3.  Click on the kebab menu, and select "_Add to existing group_"\


    <figure><img src=".gitbook/assets/image (55).png" alt=""><figcaption><p>Add one or more steps to group</p></figcaption></figure>


4.  Then from the popup modal, all your existing groups will be listed. From the list, select the group you want to add the selected steps to.\


    <figure><img src=".gitbook/assets/image (56).png" alt=""><figcaption><p>Add selected steps to existing group</p></figcaption></figure>


5. The newly added steps will be added to the end of the group.
6. You can rearrange the steps within a group by dragging the step to the desired position.

#### Removing a step from a group

You can only remove a step from a group either by "Moving the step to a parent step", or deleting the step.

To move a step to the parent (i.e to the test case where the group is being edited),&#x20;

1. [Expand the group](groups.md#viewing-the-steps-in-a-group) to the steps within it
2. Open the settings panel of the step you want to move. (➕) => ⚙️
3.  At the bottom of the settings panel, click on "_Move to Parent_". \


    <figure><img src=".gitbook/assets/image (57).png" alt=""><figcaption><p>Move a step to the parent test</p></figcaption></figure>



_**NB: If you remove a step from a group (either by deleting or moving to parent), this will affect the group across all other tests that are using this group. Therefore, use with caution.**_

_**If you do not want the changes done to the group within a test to affect other tests using the group,**_ [_**consider duplicating the group**_](groups.md#duplicating-a-group) _**to create a local copy.**_
