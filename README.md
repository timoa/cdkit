# CDKit

[CDKit][cdkit-url] is a DevOps framework that helps to deploy mobile apps (iOS and Android) to the app stores (iTunes and Google Play).

![Example of the workflow with the CI Remote for Go app][gocd-vsm-image]

It supports the cross-platform Axway / Appcelerator Titanium framework, and it's built on top of this software:

* [GO.CD][gocd-url] as a CI/CD server
* [Fastlane][fastlane-url] to manage the certificates, assets and deployment to the app stores
* [Appium][appium-url] for the UI automation tests
* [ImageMagick][imagemagick-url] for creating app stores screenshots design
* [Ansible][ansible-url] to manage the installation and updates of the GO.CD agent(s)
* [SonarQube][sonarqube-url] for code quality and security check (optional)

## Description of the components

[CDKit][cdkit-url] uses different GIT repositories to configure and handle the end-to-end deployment to the app stores.

### cdkit.gocd

This repository stores the initial configuration of the [GO.CD][gocd-url] server, the different pipelines and environment.

### [cdkit.ansible][cdkit-ansible]

To efficiently manage and maintain the [GO.CD][gocd-url] agent(s), [CDKit][cdkit-url] use [Ansible][ansible-url].

It allows you to automatically deploy a new version of Xcode (without the App Store), updates the Android SDK, installs the latest version of Java JRE/JDK, etc.

### cdkit.releasescripts

This repository is the core of the build and deployment process.

There are scripts for generate IPA file from XArchive, create app icon with the build number, change the version of the app based on the pipeline version, create a changelog between two builds (based on GIT tags), etc.

### cdkit.certificates

This repository is maintained automatically by [Fastlane][fastlane-url] and store the iOS mobile provisioning profiles, developer and production certificates and everything is encrypted.

It's need for easy management of your profiles and certificates and all the [GO.CD][gocd-url] agents. No more manual update from Xcode on each agent!

### cdkit.appstore

At the moment, this repository store the versionCode for Android.

The versionCode is updated (by a commit) every time you deploy a new version to the Google Play.

It will be replaced soon by another [Fastlane][fastlane-url] command to get the latest versionCode from the Google Play.

### cdkit.appstore.assets

[CDKit][cdkit-url] uses this repository to store the app stores assets downloaded by [Fastlane][fastlane-url] from iTunes and the Google Play.

That includes:

* App name
* Description
* Categories
* Changelogs
* Screenshots

### [cdkit.appstore.design][cdkit-appstore-design]

It's the last addition to the [CDKit][cdkit-url] framework.

This repository contains the CLI to generate the app stores screenshots.

It support themes and different devices:

* iPhone X (5.8")
* iPhone 8 Plus (5.5")
* iPad Pro (12.9")
* Google Pixel (phone)
* Nexus 9 (tablet 10.0")
* Nexus 7 2013 (tablet 7.0")

More devices are on the way:

* iPhone Xr
* iPhone Xs
* iPhone Xs Max
* iPhone 11
* iPhone 11 Pro
* iPhone 11 Pro Max
* iPad Pro 12.9 3rd gen
* Google Pixel 3
* Google Pixel C

### [cdkit.ui.automation][cdkit-ui-automation]

[CDKit][cdkit-url] uses Appium for the UI test automation.

This repository contains a small framework to launch Appium server, build your Titanium app with a different SDK version (optional), Genymotion or an iOS simulator, run your scripts in a different configuration (devices, iOS or Android version)!

I use it also to take the screenshots that I will use later with the [App Stores Design Automation tool][cdkit-appstore-design] to create the App Store and Google Play screenshots.

It's based on the [Appcelerator Appium Tests repository][appcelerator-appium-tests] (not maintained anymore).

### cdkit.titanium.app

Sample Axway / Appcelerator Titanium project that will be used to test [CDKit][cdkit-url].

The [Appium][appium-url] UI automation scripts, screenshots design, etc. will be based on this mobile app project.

## How to install CDKit

To use this framework, you will need to clone this GIT repositories:

* [cdkit.gocd][cdkit-gocd] (WIP)
* [cdkit.titanium.app][cdkit-titanium-app] (WIP)
* [cdkit.releasescripts][cdkit-releasescripts] (WIP)
* [cdkit.certificates][cdkit-certificates] (WIP)
* [cdkit.appstore][cdkit-appstore] (WIP)
* [cdkit.appstore.assets][cdkit-appstore-assets] (WIP)
* [cdkit.appstore.design][cdkit-appstore-design]
* [cdkit.ui.automation][cdkit-ui-automation]
* [cdkit.ansible][cdkit-ansible]

## TODO

* Deploy my existing scripts and create the README for each repositories
* Convert the remaining Bash scripts to Python or Golang (cdkit.releasescripts)
* Create a Docker image for the GO.CD server with the initial setup to run quickly the first pipelines

[cdkit-url]: https://cdkit.org
[cdkit-gocd]: https://github.com/timoa/cdkit.gocd
[cdkit-titanium-app]: https://github.com/timoa/cdkit.titanium.app
[cdkit-releasescripts]: https://github.com/timoa/cdkit.releasescripts
[cdkit-certificates]: https://github.com/timoa/cdkit.certificates
[cdkit-appstore]: https://github.com/timoa/cdkit.appstore
[cdkit-appstore-assets]: https://github.com/timoa/cdkit.appstore.assets
[cdkit-appstore-design]: https://github.com/timoa/cdkit.appstore.design
[cdkit-ui-automation]: https://github.com/timoa/cdkit.ui.automation
[cdkit-ansible]: https://github.com/timoa/cdkit.ansible
[gocd-vsm-image]: https://github.com/timoa/cdkit/raw/master/docs/img/visual-stream-map-example.png
[gocd-url]: https://www.gocd.org/
[ansible-url]: https://www.ansible.com/
[fastlane-url]: https://fastlane.tools/
[appium-url]: http://appium.io/
[imagemagick-url]: https://www.imagemagick.org/
[sonarqube-url]: https://www.sonarqube.org/
[appcelerator-appium-tests]: https://github.com/appcelerator/appium-tests
