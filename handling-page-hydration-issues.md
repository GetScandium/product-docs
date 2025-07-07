# Handling Page Hydration Issues

At some point, while using Scandium for automated testing, you might come across a situation where Scandium performs an action—like clicking a button or entering text—but nothing actually happens. Or you might notice that text entered into an input field suddenly disappears.

One of the most common reasons for this behavior is **poor page hydration** in the application under test.

In modern web applications, when a page loads, the browser is often served a **static** version first (just HTML). After that, the **dynamic, interactive** part is loaded and the page becomes fully functional—this process is known as **hydration**. This is common in _Server-Side Rendered_ applications.

Because Scandium interacts with pages extremely fast, it may start executing actions the moment elements appear, even though the page isn't fully "live" yet. For example, a button might look enabled, but the JavaScript event listeners haven’t been attached yet. Scandium clicks the button, but because nothing is listening for the click, nothing happens.

#### How to Spot a Hydration Issue

To check if your application is affected by poor hydration:

1. Open Chrome DevTools.
2. In the **Network** tab, throttle the network speed to **Slow 3G**.
3. Reload the page and interact with the element (e.g., click a button or type into a field) as soon as it appears.

If the button click doesn’t trigger any action or the typed text gets erased, it’s a clear sign that hydration is not complete before interaction.

#### The Right Fix

This issue is common right after a page navigation or a page that has just finished loading.

The proper solution is to ensure that **interactive elements remain disabled until the page is fully hydrated** and ready to handle user (or test) actions. You can add a reasonable [prestep delay](step-settings.md) to the step that interacts with the element waiting for hydration.

This improves both user experience and test reliability by giving the page enough time to get hydrated.
