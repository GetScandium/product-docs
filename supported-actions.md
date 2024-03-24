---
description: >-
  Scandium supports a wide range of actions right out of the box, unlike many
  other record-and-playback tools.
---

# Supported Actions

### Click

All click actions are captured during the recording of your test case.

### Hover

When recording your test case, you are likely to encounter elements which you need to hover your mouse on before you can interact with a sub-element. This hover action is often difficult to automatically detect because of the way browsers work.

However, with Scandium, you can record a hover step by simply right clicking on  the element that you need to hover on, then from the contextmenu (i.e right-click menu), select the "Add hover step" option of Scadium.

<figure><img src=".gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

> _Note:  When you add a hover step, there is a chance that the hover action might not be carried out successfully when you run test locally on your machine, depending on the kind of hover technology the element uses. This is because the browser limits scripts from being able to move mouse around physically on your machine for security reasons._
>
> _However, you can run this same  test **remotely** on our browsers and you can rest assured it will work._

### Form Inputs

Scandium supports interactions with all form elements such as text inputs, checkboxes, radio buttons, select dropdowns, textarea.

It also supports a lot of WYSIWYG editors. Scandium has been tested with many popular text editors.

> If you find that Scandium doesn't  work well with your editor of choice,  please contact our support.

### Keypress

When you press certain keys such as `Tab`, `Enter` and `Escape`, special attention is given to them, and it is usually recorded as a separate step because they likely perform an action within your page.

### Browser Navigation

During your recording, as you move from one URL to another, Scandium captures these navigations. The browser's back and forward buttons are also well-supported. Page reload is also captured and replayed when re-running your tests.

### Drag and Drop

Drag and Drop actions within a web page can be of two types:

1. Dragging and dropping one element unto another element (implemented using native HTML5 DragAndDrop API)
2. Dragging and dropping an element to any location on the page (implemented using combination of mouse actions)

Scandium supports both types of DragAndDrop out of the box without you having to do anything extra other than just dragging and dropping your items.

[Watch a  video on Scandium's Drag and Drop support](https://www.youtube.com/watch?v=u281h6j2eSo\&t=3s)

### Native Popups (Alerts)

Native alert dialogs can be a big challenge for many test automation  tools, but not for Scandium. Not only does Scandium record and replay your interaction  with these native  popups, Scandium also makes it possible to even make assertions against their content.

[Watch to learn how to interact with native alerts](https://www.youtube.com/watch?v=agwZODT5ICU)

### File Upload

With Scandium, File upload during your test is a breeze. You don't even need  to do anything special other than upload your file normally as you would on your application.

Scandium supports both manual selection of files via the `<input type='file'/>` or dropping files into supported areas.

Ordinarily, Scandium has support for a lot of file-handling libraries, but if yours doesn't  work, please contact our support.

### Multiple Windows and Tabs

Scandium supports capturing your actions even if they span multiple browser tabs or windows. During replay,  Scandium will automatically open these additional tabs or windows as needed and replay your actions in them.

### IFrames

Scandium has good support for IFrames no matter how deeply nested they are.

### Shadow DOM

Scandium supports capturing and replaying actions within Shadow DOM.

> If your page's shadow dom is deeply nested beyond one layer, or is nested within nested iframes, you might encounter issues.
>
> Please contact our support for assistance.
