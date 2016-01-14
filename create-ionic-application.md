---
layout: module
title: 제 3장&#58; Ionic 애플리케이션 만들기
---
<!--
In this module, you use the Ionic CLI (command line interface) to create a new application based on the sidemenu starter app.

## Steps

1. Open a new terminal window (Mac) or a command window (Windows), and navigate (cd) to the **ionic-tutorial** directory

1. Using the Ionic CLI, create an application named **conference** based on the **sidemenu** starter app:

    ```
    ionic start conference sidemenu
    ```

1. Navigate to the **conference** folder 

    ```
    cd conference
    ```

1. Start the application in a browser using **ionic serve**.

    ```
    ionic serve
    ```

    > NOTE: Because of cross domain policy issues (specifically when loading templates), 
    you have to load the application from a server (using the http protocol and not the file protocol). **ionic serve** is a lightweight local web server with live reload.

1. In the application, open the side menu ("hamburger" icon in the upper left corner) and select 
**Playlists**. 
Select a playlist in the list to see the details view (not much to see at this point).

    In the next modules, you will replace the playlists with a list of conference sessions retrieved from the 
    server using the REST services you experimented with in the previous module.

1. Open the side menu again and select **Login**. Click the Login button to close the window (Login is not 
implemented in the starter app).

    In the last module of this tutorial you will implement Login using **Facebook**.
-->

이번 장에서 사이드 메뉴 스타터 앱을 기반으로, 새로운 애플리케이션을 만들기 위해 Ionic CLI(Command Line Interface)를 이용합니다.

## 단계

1. 터미널(Mac)이나 실행 창(Windows)을 열고, **ionic-tutorial-ko** 디렉토리로 이동합니다.

1. Ionic CLI를 이용하여 **sidemenu** 스타터 앱을 기반으로 **conference**라는 애플리케이션을 생성합니다.

    ```
    ionic start conference sidemenu
    ```

1. **conference** 폴더로 이동합니다.

    ```
    cd conference
    ```

1. **ionic serve** 명령으로 브라우저에서 애플리케이션을 시작합니다.

    ```
    ionic serve
    ```

    > NOTE: 크로스 도메인 정책 이슈(특별히 템플릿을 로딩할 때) 때문에, 여러분은 서버로부터 애플리케이션을 로딩해야 합니다.(file 프로토콜을 사용하지 않고 http 프로토콜을 사용) **ionic serve**는 라이브 갱신이 되는 가벼운 로컬 웹서버 입니다.

1. 애플리케이션에서 슬라이드 메뉴를 열고(상단의 왼쪽 구석에 있는 "햄버거" 아이콘) **Playlists**를 선택합니다.
목록중에서 playlist를 선택하면 the details view를 볼 수 있습니다. (이것이 보이는 것이 핵심이 아닙니다.)
    다음 장에서 playlist를 이전 장에서 실험해본 REST 서비스를 이용하여 검색된 회의 세션 중 하나로 교체할 것입니다.

1. 사이드 메뉴를 다시 열고 **Login**을 선택하세요. 로그인 버튼을 클릭하면 창이 닫힙니다(로그인은 스타터 앱에서 구현되지 않습니다).

    이 튜토리얼의 마지막 장에서 여러분은 **Facebook**를 이용하여 로그인을 구현할 것입니다.

<div class="row" style="margin-top:40px;">
<div class="col-sm-12">
<a href="start-node-server.html" class="btn btn-default"><i class="glyphicon glyphicon-chevron-left"></i> 
이전</a>
<a href="create-angular-service.html" class="btn btn-default pull-right">다음 <i class="glyphicon 
glyphicon-chevron-right"></i></a>
</div>
</div>