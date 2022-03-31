# HMS Environment Preparation - Titanium Plugin (SDK 10.1.1)

A Titanium Plugin to prepare the [HMS environment ](https://developer.huawei.com/consumer/en/codelab/HMSPreparation/index.html) in your Titanium project.

This plugin is required to start using some HMS services such as [titanium-hms-push-kit](https://github.com/ikamaru/titanium-hms-push-kit) and [titanium-hms-map-kit](https://github.com/ikamaru/titanium-hms-map-kit)


## Content
* [Requirements](#requirements)
* [Preparation](#preparation)
* [Structure Of The Project](#structure-of-the-project)

## Requirements
- [x] Before you get started, you must register as a [HUAWEI developer](https://developer.huawei.com/consumer/en/) and complete identity verification on HUAWEI Developers. For details, please refer to [Registration and Verification](https://developer.huawei.com/consumer/en/doc/start/registration-and-verification-0000001053628148).
- [x] Create an app by following instructions in [Creating an AppGallery Connect Project](https://developer.huawei.com/consumer/en/doc/development/AppGallery-connect-Guides/agc-get-started#createproject) and [Adding an App to the Project](https://developer.huawei.com/consumer/en/doc/development/AppGallery-connect-Guides/agc-get-started#createapp).

## Preparation

### Console Side
- Run the keytool command to get the SHA256 fingerprint from the keystore: 
```bash
keytool -list -v -keystore hms_test.jks
```

>Note: Replace **hms_test.jks** with your keystore path
- Obtain the SHA256 fingerprint from the result:
![key](https://user-images.githubusercontent.com/61454003/101916607-7a38b700-3bc7-11eb-8ddb-c7746432dea8.png)

- On the AppGallery Connect (AGC) console of [HUAWEI Developer](https://developer.huawei.com/consumer/en/), Select your project or create a new one if you didn't do yet, then:
    -    At the bottom inside the tab **Project Setting** > **General information**, past the obtained SHA256 fingerprint, Click √ to save the fingerprint and download then the **agconnect-services.json** file.
![image](https://user-images.githubusercontent.com/61454003/101918101-3f378300-3bc9-11eb-9633-73beedb855b3.png)

### Titanium App side:
- Create a Titanium project, if it doesn't exists, using the following command:
```bash
titanium create --type app --platforms android
```
- Create a **platform\android** folder directly in your Titanium project's root folder, inside of this folder Past the **agconnect-services.json** file downloaded using HUAWEI Developer Connect.
>note: if you're using alloy create **platform\android** inside **app** folder.

- Create a **plugins** folder (same level as the **plarftom** folder) directly in your Titanium project's root folder , inside of this folder past the **com.ikamaru.ti.hms.env_preparation** folder that exists in this repo.
- Inside **tiapp.xml** add the **com.ikamaru.ti.hms.env_preparation** plugin that we downloaded in the **plugins** folder:
```xml
<plugins>
	<plugin version="3.0">com.tita.env.preparation</plugin>
</plugins>
```

## Structure Of The Project
- By following the previous steps you project must contains your project files such us the **tiapp.xml** and in the same level you must have also the following structure:
```
├───platform
│   └───android
│       ├───agconnect-services.json
└───plugins
    └───com.ikamaru.ti.hms.env_preparation
        └───2.1
            ├───hooks
            │   └───myhook.js
            └───libs
                └───helper.js
```
>note: if you're using alloy the **platform\android** folder must be inside **app** folder.

## Build
```bash
titanium build --platform android --keystore "PATH_TO_KEY_STORE.jks" --key-password "KEY_PWS" --alias "ALIAS" --store-password "STORE_PWD" 
```
> **Note**: 
> - When building for Android, make sure you have sign the app using the keystore that you used to configure your SHA256 fingerprint of your project in AppGallery Connect 
> - you can add `-T device -C all` to the above command to run on the device directly. 


## Legal

(c) 2021 by *Ikamaru*
