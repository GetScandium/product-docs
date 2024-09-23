---
description: Scandium requires the APK bundle containing your application to get started.
---

# Android

### Finding your APK file <a href="#finding-your-apk-file" id="finding-your-apk-file"></a>

#### With Android Studio <a href="#with-android-studio" id="with-android-studio"></a>

Select **Build** -> **Build APK(s)** -> **Build APK(s)** or **Build** -> **Generated Signed APK** (and following the prompts)

<figure><img src="https://docs.appetize.io/~gitbook/image?url=https%3A%2F%2F2147444700-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252F-MJUveBCJfn0GR8-hlqi%252Fuploads%252Fgit-blob-398ee77dbe6984ac05562aa58a5f6f2e014db171%252Fimage%2520%283%29%2520%281%29%2520%281%29.png%3Falt%3Dmedia&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=ac68b60e&#x26;sv=1" alt=""><figcaption><p>Building with Android Studio</p></figcaption></figure>

Once the build is complete you can locate the `.apk` file by selecting `locate` in the dialog that appears

<figure><img src="https://docs.appetize.io/~gitbook/image?url=https%3A%2F%2F2147444700-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252F-MJUveBCJfn0GR8-hlqi%252Fuploads%252Fgit-blob-1564527b364f2130ab44c8c89a9ffea05eec47cb%252FScreenshot%25202023-05-02%2520at%252015.07.06.png%3Falt%3Dmedia&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=7c8fc790&#x26;sv=1" alt=""><figcaption><p>Select <code>locate</code> in the dialog to navigate to the apk</p></figcaption></figure>

or by navigating to

```
{project name}/{app module name}/build/outputs/apk/
```

#### With Gradle <a href="#with-gradle" id="with-gradle"></a>

Generate your build with `gradle` by running the `assemble` command for your preferred app build variant e.g. `debug` variant

Copy

```
./gradlew assembleDebug
```

Once the build is complete you can locate the `.apk` file by navigating to

```
{project name}/{app module name}/build/outputs/apk/
```

### Converting AAB to APK <a href="#converting-aab-to-apk" id="converting-aab-to-apk"></a>

Scandium currently only supports `apk` files for Android. In order to get your application to work with Scandium you will need to convert your `aab` to an `apk` by making use of the [`bundletool`](https://developer.android.com/tools/bundletool) provided by Google.

**Generate Universal APKS**

```
bundletool build-apks --bundle=/<your app>/{aab name}.aab \
    --output=/{your app}/{app name}.apks \
    --mode=universal
```

**Generate Single APK file from the Universal APKs**

```
unzip -p /{your app}/{app name}.apks universal.apk > /{your app}/{app name}.apk
```

### Troubleshooting <a href="#troubleshooting" id="troubleshooting"></a>

If you are having trouble running your uploaded Android app in Scandium, we recommend trying to run the same APK on the standard Google-provided Android emulator locally over ADB.

Once your emulator is launched and available via `adb devices`, you can install it using the `install` command:

```
adb install -r {your app}.apk
```

or by simply dragging over the `apk` into the emulator window.

## Running apps that are not permitted to run on rooted device?

Scandium runs Android emulators that are very similar to the Android emulators provided by Google. So, if you encounter any issue, it's often easier to troubleshoot on the Android emulators locally, and then re-upload to Scandium.The standard Google-provided Android emulators do come with _su_. So, some apps can detect this and have limitations to run on rooted devices. If that is the issue, and you would like your app to run on Scandium, you may detect when your app is running in Scandium and skip your rooted check in that case. For convenience, we set the key "i**sAppetize**" to `true` when streaming apps.  Check below for example.

{% tabs %}
{% tab title="Java" %}
**With Intents**

The data will be passed as extras into the intent that launches your app, accessible by calling the appropriate get method (based on type) e.g.

```java
Intent intent = getIntent()
intent.getBooleanExtra("isAppetize", false);
intent.getStringExtra("stringKey");
...
```

**With SharedPreferences**

The data will also be stored in SharedPreferences under a file called `prefs.db`. This is accessible by fetching that `SharedPreferences` instance and calling the appropriate get method e.g.

```java
SharedPreferences preferences = getApplicationContext().getSharedPreferences("prefs.db", Context.MODE_PRIVATE);
preferences.getBoolean("isAppetize", false);
preferences.getString("stringKey", null);
...
```
{% endtab %}

{% tab title="Kotlin" %}
**With Intents**

The data will be passed as extras into the intent that launches your app, accessible by calling the appropriate get method (based on type) e.g.

```kotlin
intent.getBooleanExtra("isAppetize", false)
intent.getStringExtra("stringKey")
...
```

**With SharedPreferences**

The data will also be stored in SharedPreferences under a file called `prefs.db`. This is accessibly by fetching that `SharedPreferences` instance and calling the appropriate get method e.g.

Copy

```
val preferences = applicationContext.getSharedPreferences("prefs.db", Context.MODE_PRIVATE);
preferences.getBoolean("isAppetize", false)
preferences.getString("stringKey", null)
...
```

Complex types (e.g. arrays or objects) will automatically be serialized and need to be deserialized manually before using e.g. passing an object:

Copy

```
{
  "obj": { "stringKey": "value", "boolKey": true }
}
```

when queried, will return:

Copy

```
"{"stringKey":"value","boolKey":true}"
```
{% endtab %}
{% endtabs %}
