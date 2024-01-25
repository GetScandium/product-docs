---
description: Capturing and replaying file selection steps in test case recording
---

# File uploads

Scandium has full support for native file upload elements (`<input type="file">`). They are captured normally during recording and replay.

Whether you upload a single file or multiple files, Scandium is able to capture and replay these selections.

For the best file upload experience, upload files that are small in size. Recommended maximum file size: **2MB**

In the step settings of the file selection, you can see the uploaded file:

![](<.gitbook/assets/image (42).png>)

**NB:**

Files uploaded using third-party javascript libraries such as [Dropzone](https://www.dropzone.dev/) etc do not have guaranteed support at this time.
