# Why did my test fail

When running tests, it is common for them to fail. Failure could be nailed down to two main reasons:

1. A bug has been, an issue has been identified on the application being tested. This is good news for us, as the test is fulfilling the purpose for which it was created.
2. There's a flaw in the way the test was created or designed.

When a test fails, Scandium reports the failure with an identified reason for the failure.

We will go over common failure types and what could be done to remedy them.

1. Element not found
2. Element was found, but wasn't visible
3. Element was found but wasn't actionable
4. Waited for a response from iframe but no response received
5. Waited for a new page load but no new page load detected
6. Playback window was closed
7. Tab not found
8. Could not find iFrame element

### Failure Types

### Element not found

This is the most common error you will come across

#### Common causes

1. The page has not finished loading or the application is down
2. The target element has been removed from the page
3. The element's selector (e.g ID) has been changed
4. The previous step passed but the expected action did not occur. For example, if clicking on a Login button during test run is supposed to load a new page, but the username/password has changed. Clicking on the button was successful, but the login action itself wasn't successful, therefore, the next step after the login will fail.
5. The target element takes a while to appear on the page.

#### What can be done?

Check the side-by-side (baseline vs result) screenshot comparison of the step to determine if the element was visible during the test.

If the element is visible on the result screenshot, consider adding a delay on the failing step as it could have taken it time to get displayed on the page. You can add a 10-second (10000ms) delay, depending on how long you've observed it takes the element to show up.

### Element was found but not visible

The target element of the step exists on the page but is not directly visible to the user.

#### Common causes

1. The element is hidden behind another element (e.g covered by a modal)
2. The element has its CSS display property set to `none`  or visibility set to `hidden`   &#x20;
3. The height or width of the element is set to 0
4. The opacity of the element is set to 0
5. Another element must be hovered on before the target element is revealed.

#### What can be done?

Compare the result and baseline screenshots to see if the element is visible.

Update the CSS of the app to ensure the element is not hidden in error.

You can observe if this element is only temporarily hidden or covered by another element and becomes visible after a little while. If this is the case, you can add a delay to the step to give it enough time to get visible.

You can ask Scandium to interact with this element even if it is not 'visible' by updating the step and removing the visibility constraint. You do this by unchecking the '[Element should be visible'](step-settings.md) checkbox under 'Element mode' in the step settings.

### Element was found but wasn't actionable

The element was found and visible on the page, but it can not be interacted with. For example, the element is 'disabled'

#### Common causes

The target element has either a `readonly` or `disabled` property.

#### What can be done?

Update the app to remove the disabled/readonly property.

You can ask Scandium to ignore this constraint by unchecking the 'Element should be actionable' checkbox under the 'Element mode' in the step settings of the step.

### Waited for a response from iframe but no response received

During recording, the step to be executed was recorded in an iframe, but during re-execution, the iframe did not respond to the execution.

#### Common causes

1. The iframe did not load
2. The iframe no longer exists on the page. For example, that same target element is now been rendered directly on the main window instead of inside an iframe.

#### What can be done?

Re-record the affected step(s) so new updated selectors can be used for the target element.&#x20;

Delete the affected old steps afterwards.

### Waited for a new page load but no new page load detected

This error occurs if the last executed step is supposed to result into a new pageload in the browser, but the page load didn't happen.

#### Common causes

The element that was clicked on during recording caused the page to load, but during re-execution, clicking on the button didn't cause a page load. This could usually indicate that the button's function has changed.

#### What can be done?

Re-record the affected step and delete the old step.

