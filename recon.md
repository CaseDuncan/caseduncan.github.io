Title: [High] Production Google API keys and Firebase project ID hardcoded in APK
Product: mtwende.apk
Package: com.app.mtwende
Version: 13.0.1
SHA256: 258fa0e4ba31d2f4ad2a213fa01da6817e52873205fadaadc0447f6221500f01
Environment: Static analysis on distributed APK

Summary:
The APK contains hardcoded Google API keys and a production Firebase project id. Examples found:
- res/values/strings.xml: google_api_key = AIzaSyBHWon7ve3M6FW3mU0iH86QtbwJcstZcnw
- res/values/strings.xml: google_crash_reporting_api_key = AIzaSyBHWon7ve3M6FW3mU0iH86QtbwJcstZcnw
- AndroidManifest.xml meta-data: com.google.android.geo.API_KEY = AIzaSyAi3vOnoJP-0DmaTblvszbPV4_4-CwRmLI
- Firebase project id: mtwende-prod-5e6d5

Impact:
Leaked API keys can be abused to call Google APIs, resulting in quota theft, billing charges, or data access depending on key permissions. The Firebase project id facilitates reconnaissance and can increase impact when combined with leaked keys.

Steps to reproduce:
1. Download mtwende.apk and compute SHA256:
   `sha256sum mtwende.apk`
2. Decompile / inspect resources:
   `apktool d -f mtwende.apk -o mtwende_apktool`
   `grep -R "google_api_key\|API_KEY\|project_id" mtwende_apktool -n`
3. Observe keys in `res/values/strings.xml` and `AndroidManifest.xml`.

Suggested remediation:
1. **Rotate/delete** the exposed keys in Google Cloud Console immediately.
2. **Restrict** newly issued keys to the Android package name + SHA-1 signing certificate fingerprint and restrict by API.
3. Remove keys from APK and source; use backend proxies or runtime short-lived tokens issued from your servers.
4. Audit Firebase permissions and remove any excessive access.

PoC:
- Location of keys in the APK: `res/values/strings.xml` and `AndroidManifest.xml` (see grep output).
