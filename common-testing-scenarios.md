# Common Testing Scenarios

#### Can I reset browser session in between tests?

Yes, you can. Scandium provides you with a means to have your tests run from a new and clean browser session by taking advantage of the **incognito/private** browser windows.

To have Scandium record and run your tests in incognito windows, you need to turn on the incognito permission in the Scandium extension settings.

To have Scandium use incognito window for your tests, grant access to it by:

1. Opening the scandium extensions page: [chrome://extensions/?id=dokpohocljpghkmobklkccilgdiecgok](chrome://extensions/?id=dokpohocljpghkmobklkccilgdiecgok)
2. Select "**Allow in incognito**"

![image.png](https://cloud.headwayapp.co/changelogs_images/images/big/000/118/124-53604a56e81e3cafe9898ded5125cffc8104363b.png)

Creating and running your tests in incognito window ensures that a test is not affected by stored cookies, sessions, localStorage and other existing local states. It is a very critical step towards having each automated test case self-contain and isolated.

#### Are there video tutorials for using Scandium?

Yes, you can find the official Scandium tutorials on our Youtube channel: [https://www.youtube.com/@getscandium/](https://www.youtube.com/@getscandium/)

Below are some playlists demonstrating various testing scenarious:

1. [https://www.youtube.com/playlist?list=PLT7WMc3V5c-AZoQh-ltV0NNRSI7xmB5\_k](https://www.youtube.com/playlist?list=PLT7WMc3V5c-AZoQh-ltV0NNRSI7xmB5_k)
2. [https://www.youtube.com/playlist?list=PLT7WMc3V5c-BfHGRDKYQNe2ZMtHjb9xUZ](https://www.youtube.com/playlist?list=PLT7WMc3V5c-BfHGRDKYQNe2ZMtHjb9xUZ)

#### Can I record tests on Firefox Browser?

No. At the moment, the Scandium extension is only available on Google Chrome and other Chromium-based browsers such as Microsoft Edge, Brave Browser and Opera.

#### My application uses CAPTCHA, can Scandium handle that?

CAPTCHAs are designed to differentiate human users from bots, making them a challenge for automated testing tools like Scandium. Since they intentionally block automated interactions, you’ll need to implement workarounds or disable them during testing. Here are some practical solutions:

1. **Use Test Keys for External CAPTCHA Services**
   * If you’re using a service like reCAPTCHA, check their documentation for test keys that bypass validation in testing environments.
   * Alternatively, whitelist your test environment domains to exclude them from CAPTCHA checks.
2. **Disable CAPTCHAs for Tests**
   * Implement a hidden mechanism (e.g., a secret URL parameter or environment variable) that disables CAPTCHA validation when triggered by your tests.
   * Configure your system to skip CAPTCHA checks when requests come from known testing IP addresses.
3. **Test in a Controlled Environment**
   * Disable CAPTCHAs entirely in development or staging environments where automated tests run.

By implementing one of these strategies, you can maintain test automation efficiency while ensuring CAPTCHA functionality remains secure in production.

#### How can I test email OTP scenarios

Tests where you have to get a dynamic verification code from an email inbox can pose a challenge for automation. Luckily, Scandium provides you with an easy solution to handling this.

The video below shows a demonstration on how to handle OTP-email scenarios in your tests.

{% embed url="https://youtu.be/__MgmPYFODk?list=PLT7WMc3V5c-AZoQh-ltV0NNRSI7xmB5_k" %}
