📱 Critical Vulnerability: Excessive Permissions and Unauthorized Audio Recording Risk in the Cryptocurrency App com.cryptology.flutter
🔐 Vulnerability Description

Multiple critical vulnerabilities have been identified in the mobile application com.cryptology.flutter, a cryptocurrency app available for Android. These issues pose a serious risk to user privacy and security, primarily due to:

    Unjustified request of excessive permissions.

    Continuous access to the microphone through the FOREGROUNDSERVICE_MICROPHONE permission.

    Runtime access to the microphone without the user’s explicit consent.

🚨 1. Excessive Permissions

The app requests a number of permissions that are not directly related to its core functionality as a cryptocurrency exchange platform:

    READ_EXTERNAL_STORAGE

    WRITE_EXTERNAL_STORAGE

    CAMERA

    ACCESS_FINE_LOCATION

    ACCESS_COARSE_LOCATION

    WRITE_SETTINGS

    FOREGROUNDSERVICE_MICROPHONE (📢 allows continuous background audio recording)

These permissions pose a major privacy threat, potentially enabling mass collection of sensitive data and covert surveillance of users.
⚙️ 2. Permissions Granted at Installation

Upon installation, several sensitive permissions are granted automatically, with no user interaction required:

android.permission.FOREGROUNDSERVICEMICROPHONE: granted=true
android.permission.RECORD_AUDIO: granted at runtime (see section 3)
android.permission.INTERNET: granted=true
android.permission.ACCESS_NETWORK_STATE: granted=true
android.permission.USE_FINGERPRINT: granted=true
android.permission.USE_BIOMETRIC: granted=true
android.permission.ACCESS_WIFI_STATE: granted=true
android.permission.RECEIVE_BOOT_COMPLETED: granted=true
com.google.android.gms.permission.AD_ID: granted=true

The FOREGROUNDSERVICE_MICROPHONE permission is particularly concerning, as it allows continuous audio recording even while the app is in the background — without requiring any further user action.
🎙️ 3. RECORD_AUDIO Permission Granted at Runtime

During testing on a Samsung A52 device, it was confirmed that the app has RECORD_AUDIO permission enabled, without any prompt asking the user for access:

    Test Device: Samsung A52

    Permission: android.permission.RECORD_AUDIO: granted=true

    Observation: At no point was microphone access explicitly requested from the user.

⚠️ This represents a severe privacy violation and may breach data protection laws, such as the GDPR in Europe.
⚖️ Legal Considerations

Recording and processing audio data without explicit user consent may violate multiple regulations:

    General Data Protection Regulation (GDPR) – European Union

    National communication privacy laws

    One- or two-party consent laws for recordings, depending on jurisdiction

Even for purposes like marketing or analytics, clear and specific consent must be obtained and documented.
🧪 Validation Steps
🔍 APK Analysis

    Download APK:

https://apkcombo.app/en/tothemoon-buy-trade-btc/com.cryptology.flutter/download/apk

    Decompile with apktool:

apktool d com.cryptology.flutter.apk -o decrypted_apk

    Review AndroidManifest.xml for requested permissions.

📱 Device Testing

    Install the app on a Samsung A52.

    Connect the device via ADB:

adb devices
adb shell getprop ro.product.manufacturer
adb shell getprop ro.product.model

    Check granted permissions:

adb shell dumpsys package com.cryptology.flutter | grep permission

    Confirm that no prompt appears requesting microphone access during install or use.

💥 Impact
Risk Category	Description
🕵️ Privacy Violation	Recording conversations without consent
💸 Financial Data Theft	Potential access to wallet or account information
🧬 Data Manipulation	Modification of app settings without user knowledge
🧠 Personal Data Harvesting	Use of sensitive data for marketing or unknown purposes
⚠️ Full Device Compromise	Malicious use of sensors, microphone, and hardware resources
🔎 Vulnerability Classification (CVSS v3.1)
Metric	Value
Severity	CRITICAL
Attack Vector	Network
Attack Complexity	Low
Privileges Required	None
User Interaction	None
Scope	Changed
Confidentiality Impact	High
Integrity Impact	High
Availability Impact	Low
🛡️ Recommendations

    Remove unnecessary permissions from the AndroidManifest.xml.

    Request sensitive permissions only when strictly needed, and always with clear user consent.

    Improve transparency in the app’s privacy policy and permission prompts.

    Conduct external security audits and compliance reviews.

    Ensure full compliance with GDPR and other local data protection and recording laws.

📌 Conclusion

The com.cryptology.flutter application poses a severe privacy and security risk due to its ability to record audio without user consent. It is strongly recommended that the developers:

    Review and refactor the permission usage.

    Conduct a comprehensive security and privacy audit.

    Ensure compliance with data protection regulations before continuing app distribution
