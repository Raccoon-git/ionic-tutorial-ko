---
layout: module
title: 제 9장&#58; 페이스북 연동하기
---
<!--
In this module, you add Facebook integration to your application. You allow users to login with Facebook, view their profile, and share their favorite sessions on their feed.

## Step 1: Create a Facebook application

1. Login to Facebook

1. Access [https://developers.facebook.com/apps](https://developers.facebook.com/apps), and click **Add New App**

1. Select **www** as the platform

1. Type a unique name for your app and click **Create New Facebook App ID** 

1. Specify a **Category**, and click **Create App ID**

1. Click **My Apps** in the menu and select the app you just created 

1. Click **Settings** in the left navigation

1. Click the **Advanced Tab**

1. In the **OAuth Settings** section, add the following URLs in the **Valid OAuth redirect URIs** field:
    - [http://localhost:8100/oauthcallback.html](http://localhost:8100/oauthcallback.html) (for access using ionic serve)
    - [https://www.facebook.com/connect/login_success.html](https://www.facebook.com/connect/login_success.html) (for access from Cordova)

1. Click **Save Changes**  


## Step 2: Initialize OpenFB

1. Add the OpenFB files to your application
    - Copy **openfb.js** and **ngopenfb.js** from **ionic-tutorial/resources** to **conference/www/js**.
    - Copy **oauthcallback.html** and **logoutcallback.html** from **ionic-tutorial/resources** to **conference/www**.
    - In **conference/www/index.html**, add script tags to include openfb.js and ngopenfb.js (before app.js):

        ```
        <script src="js/openfb.js"></script>
        <script src="js/ngopenfb.js"></script>
        ```

        > ngOpenFB is just an Angular wrapper around the OpenFB library. It lets you use OpenFB "the Angular way":
            as an Angular service (called ngFB) instead of a global object, and using promises instead of callbacks.

1. Open **conference/www/js/app.js**, and add **ngOpenFB** as a dependency to the **starter** module:
 
    ```
    angular.module('starter', ['ionic', 'starter.controllers', 'ngOpenFB'])
    ```

1. Inject **ngFB** in the run() function declaration:

    ```
    .run(function ($ionicPlatform, ngFB) {
    ```
 
 
1. Initialize OpenFB on the first line of the run() function. Replace **YOUR&#95;FB&#95;APP_ID** with the App ID of your Facebook application.

    ```
    ngFB.init({appId: 'YOUR_FB_APP_ID'});
    ```

## Step 3: Add Facebook login

1. Open login.html in the **conference/www/templates** directory. Add a **Login with Facebook** button right after the 
existing **Log 
In** button: 

    ```
    <label class="item">
        <button class="button button-block button-positive" ng-click="fbLogin()">
        Login with Facebook
        </button>
    </label>
    ```

    > Notice that fbLogin() is called on ng-click. You define the fbLogin() function in the next step.

1. Open conference/www/js/controllers.js, and add **ngOpenFB** as a dependency to the **starter.controllers** module:
 
    ```
    angular.module('starter.controllers', ['starter.services', 'ngOpenFB'])
    ``` 

1. Inject **ngFB** in the **AppCtrl** controller:

    ```
    .controller('AppCtrl', function ($scope, $ionicModal, $timeout, ngFB) {
    ```
    
1. Add the fbLogin function in the **AppCtrl** controller (right after the 
doLogin function):

    ```
    $scope.fbLogin = function () {
        ngFB.login({scope: 'email,read_stream,publish_actions'}).then(
            function (response) {
                if (response.status === 'connected') {
                    console.log('Facebook login succeeded');
                    $scope.closeLogin();
                } else {
                    alert('Facebook login failed');
                }
            });
    };
    ```

1. Test the application. 
    - Make sure **ionic serve** (your local web server) is still running. If it's running but you closed your app page in the browser, you can reload the app by accessing the following URL: [http://localhost:8100](http://localhost:8100). 
        If it's not running, open a command prompt, navigate (cd) to the **ionic-tutorial** directory and type:
    
        ```
        ionic serve
        ```
    - In the application, open the side menu and select **Login**
    - Click the **Login with Facebook** button
    - Enter your Facebook credentials on the Facebook login screen, and authorize the application 
    - Open the browser console: you should see the **Facebook login succeeded** message

    > The next time you login, you won't be asked for your credentials again since you already have a valid token. To
     test the login process again, simply logout from Facebook. The OpenFB library has additional methods to logout 
     and revoke permissions that are beyond the scope of this tutorial.  


## Step 4: Display the User Profile

1. Create a **template** for the user profile view. In the **conference/www/templates** directory, create a new file named **profile.html** and implement it as follows:

    ```
    {% raw %}
    <ion-view view-title="Profile">
        <ion-content class="has-header">
            <div class="list card">
                <div class="item">
                    <h2>{{user.name}}</h2>
                    <p>{{user.city}}</p>
                </div>
                <div class="item item-body">
                    <img src="http://graph.facebook.com/{{user.id}}/picture?width=270&height=270"/>
                </div>
            </div>
        </ion-content>
    </ion-view>
    {% endraw %}
    ```

1. Create a **controller** for the user profile view. Open **controllers.js**, and add the following controller:

    ```
    .controller('ProfileCtrl', function ($scope, ngFB) {
        ngFB.api({
            path: '/me',
            params: {fields: 'id,name'}
        }).then(
            function (user) {
                $scope.user = user;
            },
            function (error) {
                alert('Facebook error: ' + error.error_description);
            });
    });
    ```

1. Create a **route** for the user profile view. Open **app.js**, and add the following route:

    ```
    .state('app.profile', {
        url: "/profile",
        views: {
            'menuContent': {
                templateUrl: "templates/profile.html",
                controller: "ProfileCtrl"
            }
        }
    })
    ```

1. Open **www/templates/menu.html**, and add the following menu item:

    ```
    <ion-item menu-close href="#/app/profile">
        Profile
    </ion-item>
    ```

1. Test the application:
    - Make sure **ionic serve** (your local web server) is still running. If it's running but you closed your app page in the browser, you can reload the app by accessing the following URL: [http://localhost:8100](http://localhost:8100). 
        If it's not running, open a command prompt, navigate (cd) to the **ionic-tutorial** directory and type:
    
        ```
        ionic serve
        ```
    - Open the side menu and select **Login**
    - Login with Facebook
    - Open the side menu and select **Profile**


## Step 5: Publish to your feed

1. Open **controllers.js**, and inject **ngFB** in the **SessionCtrl** definition:
 
    ```
    .controller('SessionCtrl', function ($scope, $stateParams, Session, ngFB) {
    ```

1. Add a **share()** function to the **SessionCtrl** controller:

    ```
    $scope.share = function (event) {
        ngFB.api({
            method: 'POST',
            path: '/me/feed',
            params: {
                message: "I'll be attending: '" + $scope.session.title + "' by " +
                $scope.session.speaker
            }
        }).then(
            function () {
                alert('The session was shared on Facebook');
            },
            function () {
                alert('An error occurred while sharing this session on Facebook');
            });
    };
    ```

1. Open **session.html** in the templates directory and add an **ng-click** handler to the Share button: invoke the 
share function: 

    ```
    <a class="tab-item" ng-click="share()">
        <i class="icon ion-share"></i>
        Share
    </a>
    ```

1. Test the application:
    - Make sure **ionic serve** (your local web server) is still running. If it's running but you closed your app page in the browser, you can reload the app by accessing the following URL: [http://localhost:8100](http://localhost:8100). 
        If it's not running, open a command prompt, navigate (cd) to the **ionic-tutorial** directory and type:
    
        ```
        ionic serve
        ```
    - Open the side menu and select **Login**
    - Login with Facebook
    - Open the side menu, select **Sessions**, and select a session in the list
    - Click/Tap the **Share** button
    - Check your feed on Facebook


## Step 6: Test Facebook integration on device (optional)

1. Add the **InAppBrowser** plugin used by OpenFB when running in Cordova. On the command line, navigate to the **ionic-tutorial/conference** directory and type:

    ```
    cordova plugins add org.apache.cordova.inappbrowser
    ```

1. Build your application for a specific platform following the steps described in module 8:

    ```
    ionic build ios
    ```

    and/or
 
    ```
    ionic build android
    ```
    
    If the build fails after adding the plugin, try removing and re-adding the platform. For example:
    
    ```
    ionic platform remove ios
    ionic platform add ios
    ionic build ios
    ```
 
1. Run and test your application on an iOS or Android device or emulator 
-->

이번 장에서 애플리케이션에 페이스북 연동을 추가합니다. 사용자들의 피드에 페이스북에 로그인, 프로파일 조회, 즐겨찾는 세션들을 공유하기 위해서 허가합니다.

> 이번 튜토리얼에서 연동하기 위해서 [OpenFB](https://github.com/ccoenraets/OpenFB)를 사용합니다. OpenFB는 페이스북과 자바스크립트 애플리케이션의 연동을 위한 아주 작은 라이브러리입니다. 브라우저, Crodova/PhoneGap 앱 모두 동작하고 아무런 의존성도 없습니다: Cordova에서 실행할때에 페이스북 플러그인은 필요 없습니다. 또한 페이스북 SDK조차 필요 없습니다. 더 자세한 내용은 [여기](https://github.com/ccoenraets/OpenFB)에 있습니다.

## 1단계: 페이스북 애플리케이션을 생성합니다

1. 페이스북에 로그인합니다.

1. [https://developers.facebook.com/apps](https://developers.facebook.com/apps)을 접속하여**Add New App**을 클릭합니다.

1. 플랫폼을 **www**으로 선택합니다.

1. 앱의 고유한 이름을 입력하고 **Create New Facebook App ID** 을 클릭합니다.

1. **Category**을 지정하고 **Create App ID**를 클릭합니다.

1. 메뉴에서 **My Apps**을 클릭하고 막 생성한 앱을 선택합니다.

1. 왼쪽 메뉴에서 **Settings**를 클릭합니다.

1. **Advanced Tab**를 클릭합니다.

1. **OAuth Settings** 부분에서 **Valid OAuth redirect URIs** 항목안에 다음 URL을 추가합니다:
    - [http://localhost:8100/oauthcallback.html](http://localhost:8100/oauthcallback.html) (ionic serve 사용을 위해서)
    - [https://www.facebook.com/connect/login_success.html](https://www.facebook.com/connect/login_success.html) (Cordova에서 접속을 위해서)

1. **Save Changes**를 클릭합니다.


## 2단계: OpenFB를 초기화 합니다

1. 애플리케이션에 OpenFB 파일을 추가합니다.
    - **ionic-tutorial/resources**에 있는 **openfb.js**와 **ngopenfb.js**를 **conference/www/js**으로 복사합니다.
    - **ionic-tutorial/resources**에 있는 **oauthcallback.html** 과 **logoutcallback.html**를 **conference/www**으로 복사합니다.
    - **conference/www/index.html**에서 openfb.js와 ngopenfb.js를 포함하기 위한 스크립트 태그를 추가합니다 (app.js 이전):

        ```
        <script src="js/openfb.js"></script>
        <script src="js/ngopenfb.js"></script>
        ```

        > ngOpenFB는 OpenFB 라이브러리를 Angular가 감싼 것 뿐입니다. 이렇게 OpenFS를 Angular 방법으로 사용합니다:
            Angular 서비스 (ngFB)가 전역 객체를 대신함으로써 콜백 대신 프라미스를 사용

1. **conference/www/js/app.js**를 열고 **starter** module에 의존으로 **ngOpenFB**를 추가합니다.

1. **ngFB**를 run() 함수 선언에 추가합니다.

    ```
    .run(function ($ionicPlatform, ngFB) {
    ```
 
1. run() 함수의 첫번째 줄에 OpenFB를 초기화 합니다. **YOUR&#95;FB&#95;APP_ID**를 페이스북 애플리케이션의 앱 ID로 수정합니다:

    ```
    ngFB.init({appId: 'YOUR_FB_APP_ID'});
    ```

## 3단계: 페이스북 로그인을 추가합니다

J. **conference/www/templates** 디렉토리에 있는 login.html을 엽니다. **Log In** 버튼 바로 다음에 **Login with Facebook** 버튼을 추가합니다:

    ```
    <label class="item">
        <button class="button button-block button-positive" ng-click="fbLogin()">
        Login with Facebook
        </button>
    </label>
    ```

    > fbLogin()은 ng-click에 의해서 호출됩니다. 다음 단계에서 fbLogin()을 정의합니다.

1. conference/www/js/controllers.js을 열고 **starter.controllers** module에 의존으로 **ngOpenFB**를 추가합니다.
 
    ```
    angular.module('starter.controllers', ['starter.services', 'ngOpenFB'])
    ``` 

1. **AppCtrl** 컨트롤러에 **ngFB**를 추가합니다:

    ```
    .controller('AppCtrl', function ($scope, $ionicModal, $timeout, ngFB) {
    ```

1. **AppCtrl** 컨트롤러에 fbLogin 함수를 추가합니다 (doLogin 함수 바로 다음):

    ```
    $scope.fbLogin = function () {
        ngFB.login({scope: 'email,read_stream,publish_actions'}).then(
            function (response) {
                if (response.status === 'connected') {
                    console.log('Facebook login succeeded');
                    $scope.closeLogin();
                } else {
                    alert('Facebook login failed');
                }
            });
    };
    ```

1. 애플리케이션을 테스트합니다.

    - **ionic serve** (로컬 웹 서버)가 여전히 실행중인지 확인하세요. 실행중이지만 브라우저의 앱 페이지를 닫았다면, [http://localhost:8100](http://localhost:8100) URL을 접속하여 앱을 재시작 할 수 있습니다.
        실행중이지 않다면 커맨드 프롬프트를 열고 **ionic-tutorial** 디렉토리로 이동후 입력하세요:

        ```
        ionic serve
        ```

    - 애플리케이션에서 슬라이드 메뉴를 열고 **Login**을 선택하세요
    - **Login with Facebook** 버튼을 클릭하세요
    - 페이스북 로그인 화면에서 인증정보를 입력하고 애플리케이션을 허가하세요
    - 브라우저 콘솔을 열고 **Facebook login succeeded** 메세지를 확인하세요

    > 다음번 로그인에서 이미 올바른 토큰을 발급받은 이후에 인증정보를 다시 물어보지 않을 것입니다. 로그인을 또 다시 테스트하기 위해서 페이스북에서 로그아웃을 하세요. OpenFB 라이브러리는 로그아웃과 이번 튜토리얼의 영역을 넘어 권환을 폐지하는 추가적인 방법을 가지고 있습니다.


## 4단계: 사용자 프로파일을 보여줍니다

1. 사용자 프로파일 뷰를 위한 **템플릿**을 생성합니다. **conference/www/templates**에서 **profile.html**의 파일을 새로 만들고 다음과 같이 템플릿을 작성합니다:

    ```
    {% raw %}
    <ion-view view-title="Profile">
        <ion-content class="has-header">
            <div class="list card">
                <div class="item">
                    <h2>{{user.name}}</h2>
                    <p>{{user.city}}</p>
                </div>
                <div class="item item-body">
                    <img src="http://graph.facebook.com/{{user.id}}/picture?width=270&height=270"/>
                </div>
            </div>
        </ion-content>
    </ion-view>
    {% endraw %}
    ```

1. 사용자 프로파일 뷰를 위해서 **컨트롤러**를 생성합니다. **controllers.js**를 열고 다음과 같이 컨트롤러를 작성합니다:

    ```
    .controller('ProfileCtrl', function ($scope, ngFB) {
        ngFB.api({
            path: '/me',
            params: {fields: 'id,name'}
        }).then(
            function (user) {
                $scope.user = user;
            },
            function (error) {
                alert('Facebook error: ' + error.error_description);
            });
    });
    ```

1. 사용자 프로파일 뷰를 위해서 **라우트**를 생성합니다. **app.js**를 열고 다음과 같이 라우트를 작성합니다:

    ```
    .state('app.profile', {
        url: "/profile",
        views: {
            'menuContent': {
                templateUrl: "templates/profile.html",
                controller: "ProfileCtrl"
            }
        }
    })
    ```

1. **www/templates/menu.html**를 열고 다음과 같이 menu item을 작성합니다:

    ```
    <ion-item menu-close href="#/app/profile">
        Profile
    </ion-item>
    ```

1. 애플리케이션을 테스트합니다.
    - **ionic serve** (로컬 웹 서버)가 여전히 실행중인지 확인하세요. 실행중이지만 브라우저의 앱 페이지를 닫았다면, [http://localhost:8100](http://localhost:8100) URL을 접속하여 앱을 재시작 할 수 있습니다.
        실행중이지 않다면 커맨드 프롬프트를 열고 **ionic-tutorial** 디렉토리로 이동후 입력하세요:

        ```
        ionic serve
        ```

    - 애플리케이션에서 슬라이드 메뉴를 열고 **Login**을 선택하세요
    - 페이스북에 로그인 하세요
    - 슬라이드 메뉴를 열고 **Profile**를 선탁하세요.


## 5단계: 피드에 발행하기

1. **controllers.js**를 열고 **SessionCtrl** 정의에 **ngFB**를 추가하세요:
 
    ```
    .controller('SessionCtrl', function ($scope, $stateParams, Session, ngFB) {
    ```

1. **share()** 함수를 **SessionCtrl** 컨트롤러에 추가하세요:

    ```
    $scope.share = function (event) {
        ngFB.api({
            method: 'POST',
            path: '/me/feed',
            params: {
                message: "I'll be attending: '" + $scope.session.title + "' by " +
                $scope.session.speaker
            }
        }).then(
            function () {
                alert('The session was shared on Facebook');
            },
            function () {
                alert('An error occurred while sharing this session on Facebook');
            });
    };
    ```

1. 템플릿 디렉토리의 **session.html**을 열고 share 함수를 실행할 공유 버튼을 위해 **ng-click**을 추가하세요:

    ```
    <a class="tab-item" ng-click="share()">
        <i class="icon ion-share"></i>
        Share
    </a>
    ```

1. 애플리케이션을 테스트합니다.
    - **ionic serve** (로컬 웹 서버)가 여전히 실행중인지 확인하세요. 실행중이지만 브라우저의 앱 페이지를 닫았다면, [http://localhost:8100](http://localhost:8100) URL을 접속하여 앱을 재시작 할 수 있습니다.
        실행중이지 않다면 커맨드 프롬프트를 열고 **ionic-tutorial** 디렉토리로 이동후 입력하세요:

        ```
        ionic serve
        ```

    - 애플리케이션에서 슬라이드 메뉴를 열고 **Login**을 선택하세요
    - 페이스북에 로그인 하세요
    - 슬라이드 메뉴를 열고 **Sessions**를 선택하고 목록중에 한 세션을 선택합니다
    - **Share** 버튼을 클릭/탭 합니다
    - 페이스북 피드를 확인하세요


## 6단계: 장치에서 페이스북 연동을 테스트하세요 (선택)

1. Cordova가 실행할 때 OpenFB가 사용하는 **InAppBrowser** 플러그인을 추가하세요. 커맨드 라인에서 **ionic-tutorial/conference** 디렉토리로 이동하고 입력하세요:

    ```
    cordova plugins add org.apache.cordova.inappbrowser
    ```

1. 제 8장에서 설명한 단계를 따라서 특정한 플랫폼에 맞는 애플리케이션을 빌드하세요:

    ```
    ionic build ios
    ```

    또는
 
    ```
    ionic build android
    ```

    플러그인을 추가한 후에 빌드가 실패했다면, 플랫폼을 삭제하고 다시 추가하세요. 예를들면:
    
    ```
    ionic platform remove ios
    ionic platform add ios
    ionic build ios
    ```

1. iOS나 Android 장치 또는 에뮬레이터에서 애플리케이션을 실행하고 테스트하세요.

<div class="row" style="margin-top:40px;">
<div class="col-sm-12">
<a href="build-ionic-project.html" class="btn btn-default"><i class="glyphicon glyphicon-chevron-left"></i> 
이전</a>
</div>
</div>
