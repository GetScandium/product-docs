---
description: Customizing an individual step within a test.
---

# Step settings

After recording your test, Scandium allows you review and modify the details of each step within the test.

To access the settings of a step, click on the plus (+) button on the step, then click on the settings icon in the expanded options.

<figure><img src=".gitbook/assets/image (34).png" alt=""><figcaption></figcaption></figure>

This will reveal the settings sidebar.

The following are options you can customize on a step.

1. **Title**: A descriptive title for the step
2. **Text to Assign:** The input value of the step (if the target element of the step is an input editable field)
3. **Target element:** CSS Selector string to identify the target element of the step.
4. **Element mode**:
   1. **Element should be visible**: The target element must be visible on the page i.e not hidden, not blocked by another element.
   2. **Element should be actionable**: In addition to the target element being visible, it must also be actionable i.e not disabled or have readonly property.
5. **Failure mode (When this step fails):** Determines what should happen to the test if the step fails. There are three (3) modes available:
   1. **Fail test immediately:** The test will be aborted and reported as failed. Steps after the failed step will not be executed.
   2. **Fail and continue:** The test will be reported as failed, but test will not be aborted. Steps after the failed step will still be executed.
   3. **Ignore failure:** The step will simply be ignored. The test will not be reported as failed, and steps after the failed step will be executed.
6. **Precondition mode (When to run this step):** Sets a condition that is first evaluated before determining if the step should be executed or not. If the evaluation of the condition results to true, the step will be executed, otherwise, the step will be skipped. You can set the following conditions on a step:
   1. **Always run:** No condition is attached to the step, the step will always run.
   2. **Never run (skip):** The step will be skipped during execution. This can be used if you do not want to delete the step permanently.
   3. **Element visible:** _This requires an additional css selector._ If the element specified in the selector is found and visible on the page, the step will be executed. If not found, the step will be skipped.
   4. **Element not visible:** _This requires an additional css selector._ If the element specified by the selector is visible on the page, the step **will not** be executed, but if not found, the step will be executed.
   5. **Element contains text:** _This requires an additional css selector and a string to check for._ If the the element specified by the css selector contains the specified string, the step will be executed. If it doesn't contain the string, the step will be skipped.
   6. **Page title matches:** _This requires an additional page title string._ If the specified page title string matches the current page title, the step will be executed, otherwise, the step will be skipped.
   7. **Page URL matches:** _This requires an additional URL string._ If the current page URL matches the specified url string, the step will be executed, otherwise, the step will be skipped.
7. **Prestep delay:** To set how long (in milliseconds) should Scandium wait for before attempting to execute the step.\
   _**Reminder: 1000 milliseconds = 1 second**_
8. **Step timeout:** If a target element is not immediately found on a page, Scandium keeps trying to fetch the element until it either finds it or the timeout expires. If and after the timeout expires, Scandium will then report the step as a failure. You can control how long you want to Scandium to wait while attempting to fetch the target element of the step. This property is also in milliseconds.
9. **Scroll into view:** To control what should happen if the target element is not currently within the visible viewport. If this setting is checked, Scandium will scroll to the element and show it within the viewport.
10. **Delete:** To delete a step permanently. Use with caution, this action is irreversible. If you do not intend to permanently delete a step, use the "Never run" precondition.

### Applying settings to multiple steps

There are certain customizations that you might need to apply to multiple steps at a time. Settings like: prestep delay, step timeout, failure mode and wait mode.

You can achieve this by ticking the checkboxes on the steps you want to edit, then click on the floating options icon (vertical ellipsis), then click on 'Edit' in the dropdown menu.

Make the changes you want to apply.

<figure><img src=".gitbook/assets/scandium edit multiple steps.gif" alt=""><figcaption><p>Edit multiple steps at once</p></figcaption></figure>
