# CDKit

CDKit is a framework that helps to deploy mobile apps (iOS and Android) to the app stores (iTunes and Goole Play).

![Example of the workflow with the CI Remote for Go app](https://github.com/timoa/cdkit/raw/master/docs/img/visual-stream-map-example.png)

It supports the cross-platform Axway / Appcelerator Titanium framework, and it's built on top of this software:

- GO.CD as a CI/CD server
- Fastlane to manage the certificates, assets and deployment to the app stores
- Appium for the UI automation tests
- ImageMagick for creating app stores screenshots design
- Ansible to manage the installation and updates of the GO.CD agent(s)
- SonarQube for code quality check (optional)


## Description of the components

CDKit uses different GIT repositories to configure and handle the end-to-end deployment to the app stores.

### cdkit.gocd

This repository stores the initial configuration of the GO.CD server, the different pipelines and environment.

### [cdkit.ansible](https://github.com/timoa/cdkit.ansible)

To efficiently manage and maintain the GO.CD agent(s), CDKit use Ansible.

It allows you to automatically deploy a new version of Xcode (without the App Store), updates the Android SDK, installs the latest version of Java JRE/JDK, etc.

### cdkit.releasescripts

This repository is the core of the build and deployment process.

There are scripts for generate IPA file from XArchive, create app icon with the build number, change the version of the app based on the pipeline version, create a changelog between two builds (based on GIT tags), etc.

### cdkit.certificates

This repository is maintained automatically by Fastlane and store the iOS mobile provisioning profiles, developer and production certificates and everything is encrypted.

It's need for easy management of your profiles and certificates and all the GO.CD agents. No more manual update from Xcode on each agent!

### cdkit.appstore

At the moment, this repository store the versionCode for Android.

The versionCode is updated (by a commit) every time you deploy a new version to the Google Play.

It will be replaced soon by another Fastlane command to get the latest versionCode from the Google Play.

### cdkit.appstore.assets

CDKit uses this repository to store the app stores assets downloaded by Fastlane from iTunes and the Google Play.

That includes:

- App name
- Description
- Categories
- Changelogs
- Screenshots

### cdkit.appstore.design

It's the last addition to the CDKit framework.

This repository contains the CLI to generate the app stores screenshots.

It support themes and different devices:

- iPhone X (5.8")
- iPhone 8 Plus (5.5")
- iPad Pro (12.9")
- Google Pixel (phone)
- Nexus 9 (tablet 10.0")
- Nexus 7 2013 (tablet 7.0")

### cdkit.ui.automation

CDKit uses Appium for the UI automation.

This repository contains a small framework to launch Appium server, build your Titanium app with a different SDK version (optional), Genymotion or an iOS simulator, run your scripts in a different configuration (devices, iOS or Android API version)!

It's based on the [Appcelerator Appium Tests repository](https://github.com/appcelerator/appium-tests) (not maintained anymore).

### cdkit.titanium.app

Sample Axway / Appcelerator Titanium project that will be used to test CDKit.

The Appium UI automation scripts, screenshots design, etc. will be based on this mobile app project.


## How to install CDKit
To use this framework, you will need to clone this GIT repositories:
- [cdkit.gocd](https://github.com/timoa/cdkit.gocd) (WIP)
- [cdkit.titanium.app](https://github.com/timoa/cdkit.titanium.app) (WIP)
- [cdkit.releasescripts](https://github.com/timoa/cdkit.releasescripts) (WIP)
- [cdkit.certificates](https://github.com/timoa/cdkit.certificates) (WIP)
- [cdkit.appstore](https://github.com/timoa/cdkit.appstore) (WIP)
- [cdkit.appstore.assets](https://github.com/timoa/cdkit.appstore.assets) (WIP)
- [cdkit.appstore.design](https://github.com/timoa/cdkit.appstore.design) (WIP)
- [cdkit.ui.automation](https://github.com/timoa/cdkit.ui.automation) (WIP)
- [cdkit.ansible](https://github.com/timoa/cdkit.ansible)

## TODO

- Deploy my existing scripts and create the README for each repositories
- Convert the remaining Bash scripts to Python (cdkit.releasescripts)
- Create and deploy a single page website to cdkit.org (domain name purchased)
- Create a Docker image for the GO.CD server with the initial setup to run quickly the first pipelines