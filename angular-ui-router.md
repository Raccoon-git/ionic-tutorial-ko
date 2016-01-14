---
layout: module
title: 제 7장&#58; 라우팅 구현하기
---
<!--
In this module, you add two new routes (states) to the application: app.sessions loads the session list view, and app.session loads the session details view.

## Step 1: Define the app.sessions route 

1. Open **app.js** in conference/www/js

1. Delete the **app.playlists** state
 
1. Replace it with an **app.sessions** state defined as follows:

    ```
    .state('app.sessions', {
      url: "/sessions",
      views: {
          'menuContent': {
              templateUrl: "templates/sessions.html",
              controller: 'SessionsCtrl'
          }
      }
    })
    ```

## Step 2: Define the app.session route 

1. Delete the **app.single** state
 
1. Replace it with an app.session state defined as follows:

    ```
    .state('app.session', {
        url: "/sessions/:sessionId",
        views: {
            'menuContent': {
              templateUrl: "templates/session.html",
              controller: 'SessionCtrl'
          }
        }
    });
    ```

## Step 3: Modify the default route 

Modify the fallback route to default to the list of sessions (last line in app.js):

```
$urlRouterProvider.otherwise('/app/sessions');
```

## Step 4: Modify the side menu 

1. Open **menu.html** in conference/www/templates

1. Modify the Playlists menu item as follows (modify both the item label and the **href**):

    ```
    <ion-item menu-close href="#/app/sessions">
        Sessions
    </ion-item>
    ```

## Step 5: Test the application

1. Make sure **ionic serve** (your local web server) is still running.
    - If it's running but you closed your app page in the browser, you can reload the app by loading the following URL: [http://localhost:8100](http://localhost:8100)
    - If it's not running, open a command prompt, navigate (cd) to the **ionic-tutorial** directory and type:

        ```
        ionic serve
        ```
    
1. In the conference application, open the side menu ("Hamburger" icon in the upper left corner) and select **Sessions**. Select a session in the list
 to see the session details.
-->

이번 장에서 세션 리스트 뷰를 로딩하는 app.sessions과 세션 디테일 뷰를 로딩하는 app.session, 두 개의 라우트(state)를 애플리케이션에 구현합니다.

## 1단계: app.sessions의 라우트를 정의합니다.

1. conference/www/js에 있는 **app.js**를 엽니다.

1. **app.playlists** state를 삭제합니다.
 
1. **app.sessions** state 다음과 같이 작성합니다:

    ```
    .state('app.sessions', {
      url: "/sessions",
      views: {
          'menuContent': {
              templateUrl: "templates/sessions.html",
              controller: 'SessionsCtrl'
          }
      }
    })
    ```

## Step 2: app.session의 라우트를 정의합니다.

1.**app.single** state를 삭제합니다.

1. app.session state를 다음과 같이 작성합니다.

    ```
    .state('app.session', {
        url: "/sessions/:sessionId",
        views: {
            'menuContent': {
              templateUrl: "templates/session.html",
              controller: 'SessionCtrl'
          }
        }
    });
    ```

## 3단계: 기본 라우트를 수정합니다.

기본으로 세션 목록이 나오도록 라우트를 수정합니다 (app.js의 마지막 줄):

```
$urlRouterProvider.otherwise('/app/sessions');
```

## 4단계: 슬라이드 메뉴를 수정합니다.

1. conference/www/templates에서 **menu.html**를 엽니다.

1. 다음과 같이 Playlists menu item을 수정합니다 (item label과 **href**도 함께 수정합니다):

    ```
    <ion-item menu-close href="#/app/sessions">
        Sessions
    </ion-item>
    ```

## 5단계: 애플리케이션을 테스트합니다.

1. **ionic serve** (로컬 웹 서버)가 여전히 실행중인지 확인하세요.
    - 실행중이지만 브라우저의 앱 페이지를 닫았다면, [http://localhost:8100](http://localhost:8100) URL을 접속하여 앱을 재시작 할 수 있습니다.
    - 실행중이지 않다면 커맨드 프롬프트를 열고 **ionic-tutorial** 디렉토리로 이동후 입력하세요:

        ```
        ionic serve
        ```

1. 회의 앱에서 슬라이드 메뉴를 열고(죄측 상단 구석에 있는 "햄버거" 아이콘) **Sessions**를 선탁하세요. 자세한 내용을 보기 위해서 목록중에 한 세션을 선택하세요.


<div class="row" style="margin-top:40px;">
<div class="col-sm-12">
<a href="create-ionic-template.html" class="btn btn-default"><i class="glyphicon glyphicon-chevron-left"></i> 
이전</a>
<a href="build-ionic-project.html" class="btn btn-default pull-right">다음 <i class="glyphicon 
glyphicon-chevron-right"></i></a>
</div>
</div>


