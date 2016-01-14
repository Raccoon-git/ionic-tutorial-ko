---
layout: module
title: 제 4장&#58; 세션 서비스 생성하기
---

<!--
In the sidemenu starter app, the playlists are hardcoded in controllers.js. In this module, you create a Session service that uses the [Angular resource module](https://docs.angularjs.org/api/ngResource/service/$resource) (ngResource) to retrieve the conference sessions using REST services. 

## Steps

1. In the **conference/www/js** directory, create a file named **services.js**

1. In services.js, define a **module** named **starter.services** with a dependency on ngResource:

    ```
    angular.module('starter.services', ['ngResource'])
    ```

1. In that module, define a **service** named **Session** that uses the Angular resource module to provide access to the REST services at the specified endpoint:

    ```
    angular.module('starter.services', ['ngResource'])
    
    .factory('Session', function ($resource) {
        return $resource('http://localhost:5000/sessions/:sessionId');
    });
    ```
    
    > In a real-life application, you would typically externalize the server parameters in a config module.

1. The starter.services module you just created has a dependency on the Angular resource module which is
 not included by default. Open index.html and add a script tag to include **angular-resource.min.js** (right after 
 ionic-bundle.js):

    ```
    <script src="lib/ionic/js/angular/angular-resource.min.js"></script>
    ```

1. Add a script tag to include the **services.js** file you just created (right after app.js):

    ```
    <script src="js/services.js"></script>
    ```
-->

스타터 앱의 슬라이드 메뉴에서 재생목록은 controllers.js에 하드코딩 되었습니다.
이번 장에서 REST 서비스를 이용하여 회의 세션을 검색하기 위해 [Angular 리소스 모듈](https://docs.angularjs.org/api/ngResource/service/$resource) (ngResource)을 이용하여 세션 서비스를 생성합니다.

## 단계

1. **conference/www/js** 디렉토리에서 **services.js** 이름의 파일을 생성합니다.

1. services.js에서 **starter.services**라는 이름으로 **module**을 ngResource 종속과 함께 정의합니다:

    ```
    angular.module('starter.services', ['ngResource'])
    ```

1. 이번 장에서 지정된 endpoint에 REST 서비스로 접속을 제공하기 위한 Angular 리소스 모듈을 사용하는 **서비스**를 **Session**이란 이름으로 정의합니다.

    ```
    angular.module('starter.services', ['ngResource'])
    
    .factory('Session', function ($resource) {
        return $resource('http://localhost:5000/sessions/:sessionId');
    });
    ```

    > 실제로 구동되는 애플리케이션에선 보통 config module에 서버 파라미터를 기록하는 것이 좋습니다.

1. 막 생성된 starter.services 모듈은 기본적으로 포함되지 않은 Angular 리소스 모듈에 의존성을 가집니다. index.html을 열고 **angular-resource.min.js**를 포함하는 스크립트 태그를 추가합니다. (ionic-bundle.js 이후)

    ```
    <script src="lib/ionic/js/angular/angular-resource.min.js"></script>
    ```

1. 방금 생성한 **services.js** 파일을 포함하는 스크립트 태그를 추가합니다. (app.js 이후)

    ```
    <script src="js/services.js"></script>
    ```


<div class="row" style="margin-top:40px;">
<div class="col-sm-12">
<a href="create-ionic-application.html" class="btn btn-default"><i class="glyphicon glyphicon-chevron-left"></i> 
이전</a>
<a href="create-angular-controller.html" class="btn btn-default pull-right">다음 <i class="glyphicon 
glyphicon-chevron-right"></i></a>
</div>
</div>


