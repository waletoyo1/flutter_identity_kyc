# flutter_identity_kyc

IdentityPass KYC Checkout flutter Wrapper

# Getting Started

Install package by adding  flutter_identity_kyc to your pubspec.yaml file


# KYC Widget
```dart

FlutterIdentityKyc.showWidget(InputParamters(
    merchantKey: "your merchant public key",
    email: "your email address",
    firstName: "your first name",
    lastName: "your last name",
    userRef:"unique user ref",
    onCancel: (response) => {print(response)},
    onVerified: (response) => {print(response)},
    onError: (error) => print(error))),
)
```


# Requirement
# Android

Add the following permission to your android "AndroidManifest.xml" file
```xml
 <uses-permission android:name="android.permission.INTERNET" />
 <uses-permission android:name="android.permission.RECORD_AUDIO" />
 <uses-permission android:name="android.permission.MODIFY_AUDIO_SETTINGS" />
 <uses-permission android:name="android.permission.CAMERA" />
 <uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
 <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
 <uses-permission android:name="android.permission.VIDEO_CAPTURE" />
```

# IOS

Add the following permission to your android "info.plist" file
```plist
    <key>NSPhotoLibraryUsageDescription</key>
    <string>App needs access to photo lib for profile images</string>
    <key>NSCameraUsageDescription</key>
    <string>To capture profile photo please grant camera access</string>
```


# Sample implementation
```dart
import 'package:flutter/material.dart';
import 'package:flutter_identity_kyc/flutter_identity_kyc.dart';
import 'package:permission_handler/permission_handler.dart';

void main() {
  runApp(MaterialApp(home: MyApp()));
}

class MyApp extends StatefulWidget {
  @override
  _MyAppState createState() => _MyAppState();
}

class _MyAppState extends State<MyApp> {
  @override
  void initState() {
    super.initState();
    requestPermissions();
  }

  Future<void> Function() requestPermissions = () async {
    await Permission.camera.request().isGranted;

    await Permission.microphone.request();
  };

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
        home: Scaffold(
            body: Center(
                child: ElevatedButton(
      style: null,
      onPressed: () {
        FlutterIdentityKyc.showWidget(InputParameters(
            context: context,
            merchantKey: "",
            firstName: "",
            lastName: "",
            email: "",
            userRef: "",
            onCancel: (response) {
              print(response);
            },
            onVerified: (response) {
              print(response);
            },
            onError: (error) => print(error)));
      },
      child: Text('Verify My Identity'),
    ))));
  }
}
```
