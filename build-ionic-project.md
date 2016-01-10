---
layout: module
title: 제 8장&#58; 애플리케이션 빌드하기
---

<!--
This module is optional. To build the application for iOS and/or Android, you need the iOS SDK and/or the Android SDK 
installed on your system.

## Building for iOS

> You need the iOS SDK installed on your computer to build an iOS version of your application 
using the steps below.

1. On the command line, make sure you are in the **ionic-tutorial/conference** directory

1. Add support for the iOS platform:

    ```
    ionic platform add ios
    ```

    > This step is not required with recent versions of the Ionic CLI because the ios platform is installed by default

1. Build the project:

    ```
    ionic build ios
    ```

1. Open **conference.xcodeproj** in the **conference/platforms/ios** directory

1. In Xcode, run the application on a device connected to your computer or in the iOS emulator

## Building for Android

> You need the Android SDK installed on your computer to build an Android version of your 
application using the steps below.

1. Make sure the Android SDK and the ant build tool are available on your system. The Android SDK is available [here](http://developer.android.com/sdk/index.html). **Both the android and ant tools must be available in your path**. To test your configuration, you should be able to execute both **android** and **ant** from the command line.

1. On the command line, make sure you are in the **ionic-tutorial/conference** directory

1. Add support for the Android platform:

    ```
    ionic platform add android
    ```

1. Build the project:

    ```
    ionic build android
    ```

    The project is built in the **conference/platforms/android** folder


1. To build and run the application on an Android device connected to your computer using a USB cable:

    ```
    ionic run android
    ```

1. To build and run the application in the Android emulator:

    ```
    ionic emulate android
    ```
-->

이번 장은 선택적입니다. iOS와 Android를 위한 애플리케이션을 빌드하기 위해서, iOS SDK와 Android SDK가 시스템에 설치가 되어있어야 합니다.

## IOS 빌드하기

> 아래의 단계를 따라 iOS 버젼의 애플리케이션을 빌드하기 위해서 컴퓨터에 iOS SDK가 설치되어야 합니다.

1. 커맨드 라인에서 **ionic-tutorial/conference** 디렉토리에 있는지 확인하세요.

1. iOS 플랫폼 지원을 추가하세요:

    ```
    ionic platform add ios
    ```

    > 이번 단계는 최근 버전의 Ionic CLI에서는 기본적으로 ios 플랫폼이 설치되어 있기때문에 필수는 아닙니다

1. 프로젝트를 빌드합니다:

    ```
    ionic build ios
    ```

1. **conference/platforms/ios** 디렉토리에서 **conference.xcodeproj**을 엽니다.

1. Xcode에서 컴퓨터에 접속된 장치나 iOS 에뮬레이터에서 애플리케이션을 실행합니다.


## Android 빌드하기

> 아래의 단계를 따라 Android 버젼의 애플리케이션을 빌드하기 위해서 컴퓨터에 Android SDK가 설치되어야 합니다.

1. 시스템에 Android SDK와 ant build tool이 사용 가능한지 확인하세요. Android SDK는 [여기](http://developer.android.com/sdk/index.html)에서 사용가능합니다. **android와 ant tools은 반드시 여러분의 path에서 사용이 가능해야 합니다**. 설정을 테스트하기 위해 커맨드 라인에서 **android**와 **and** 모두가 실행 가능해야 합니다.

1. 커맨드 라인에서 **ionic-tutorial/conference** 디렉토리에 있는지 확인하세요.

1. Android 플랫폼 지원을 추가하세요:

    ```
    ionic platform add android
    ```

1. 프로젝트를 빌드합니다:

    ```
    ionic build android
    ```

    프로젝트는 **conference/platforms/android** 폴더에 빌드되었습니다.

1. USB cable를 이용하여 연결된 Android 장치에서 실행합니다:

    ```
    ionic run android
    ```

1. Android 에뮬레이터에서 실행합니다.

    ```
    ionic emulate android
    ```


<div class="row" style="margin-top:40px;">
<div class="col-sm-12">
<a href="angular-ui-router.html" class="btn btn-default"><i class="glyphicon glyphicon-chevron-left"></i> 
이전</a>
<a href="ionic-facebook-integration.html" class="btn btn-default pull-right">다음 <i class="glyphicon 
glyphicon-chevron-right"></i></a>
</div>
</div>


