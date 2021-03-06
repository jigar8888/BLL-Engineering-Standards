# Blue Label Labs - Mobile Standards
- Author: [Bobby Gill](https://www.bluelabellabs.com/team/bobby-gill/), [Dulio Denis](https://www.bluelabellabs.com/team/dulio-denis/)
- Version: 1.0
---

### 1. Localization Strings
Use Localization.strings (and the Android equivalent) files for all copy within an app.

All copy in alert messages/UI should be localizable. Do not hard code any strings into source code, everything should be derived from a localization file.
Provide the strings file to the PM so they can proof the strings.

### 2. Crash Reporting
Firebase Crashlytics should be integrated into every build.
- dSyms provided for every new TestFlight build and uploaded to Firebase.

- Use API Key: b53fcf08df9b183b382153735d57a10862fc5348

### 3. App Identifiers
- Every project will need one sandbox and one production identifier.

- Production: \<App Name>
- Sandbox: \<App Name> - Sandbox

### 4. CocoaPods
Use CocoaPods (when available) for integrating 3rd party libraries into iOS apps.

- CocoaPods should be checked into the Git source tree.

### 5. Passwords & Security
Passwords, and any other secure login information, **must** be stored in the iOS Keychain or Android Keystore
- Access tokens received from web services must also be stored in the keychain and not in UserDefaults.
- If the Android device does not have a passcode/pin enabled, then encrypt the password data and store into the preferences. Only do this if the passcode/pin isn’t setup and thus Android keystore isn’t available.

Android code should be protected with proguard.
- Ensure code obfuscation is turned on.

### 6. Handling User Sessions
- When a user logs in to a web service and receives a OAuth access token, this access token **must** be stored within the platform keychain and not in UserDefaults.
- Unless otherwise specified by the client, OAuth access tokens should be set with an expiry time of at least 1 month.
- Whenever a token is expired or is no longer accepted by the web service, the mobile app **must** invalidate the token from the keychain and present the user with the login screen.
- When a user chooses to logout of an app, this should be done by invalidating and deleting the locally stored access token and then optionally a call to the web service to invalidate any push device tokens. In the case where the call to invalidate push token on the web service fails due to an invalid token, the app **must not** display any authentication error to the user.  