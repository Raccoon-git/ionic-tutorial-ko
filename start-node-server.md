---
layout: module
title: 제 2장&#58; Node 서버 시작
---
<!--
In this module, you install and start a Node.js server that exposes the conference data (sessions and speakers) through a set of REST services.

## Steps

1. Download the supporting files for this tutorial [here](https://github.com/ccoenraets/ionic-tutorial/archive/master.zip), or clone the repository:

    ```
    git clone https://github.com/ccoenraets/ionic-tutorial
    ```

    > If you downloaded the zip file, unzip it anywhere on your file system.

1. Open a terminal window (Mac) or a command window (Windows), and navigate (cd) to the **ionic-tutorial/server** directory

1. Install the server dependencies:
    ```
    npm install
    ```
1. Start the server:

    ```
    node server
    ```
  
    > If you get an error, make sure you don't have another server listening on port 5000.

1. Test the REST services. Open a browser and access the following URLs:
    - [http://localhost:5000/sessions](http://localhost:5000/sessions) (for a list of conference sessions returned as a JSON document)
    - [http://localhost:5000/sessions/1](http://localhost:5000/sessions/1) (for information about a specific session )
-->

이번 장에서 회의 데이터(세션과 발표자)를 REST 서비스들을 통해서 제공할 Node.js 서버를 설치하고 시작합니다.

## 단계

1. 이 튜토리얼을 위한 파일을 [다운로드](https://github.com/ccoenraets/ionic-tutorial/archive/master.zip) 받거나 다음의 레파지토리를 복제합니다:

    ```
    git clone https://github.com/harryoh/ionic-tutorial-ko
    ```

    > zip 파일을 내려받는다면 여러분의 시스템에 압축을 해제해주세요.

1. 터미널(Mac)이나 실행 창(Windows)을 열고 **ionic-tutorial/server** 디렉토리로 이동하세요.

1. 서버의 의존성 패키지를 설치합니다.

    ```
    npm install
    ```

1. 서버를 시작합니다:

    ```
    node server
    ```
  
    > 만약 에러가 난다면, 다른 서버가 5000 포트를 사용하는지 확인해보세요.

1. REST 서비스를 테스트합니다. 브라우저를 열고 다음의 URL로 접속합니다.
    - [http://localhost:5000/sessions](http://localhost:5000/sessions) (회의 세션 목록을 위해 JSON 형태로 반환한다.)
    - [http://localhost:5000/sessions/1](http://localhost:5000/sessions/1) (특정한 세션에 대한 정보)


<div class="row" style="margin-top:40px;">
<div class="col-sm-12">
<a href="install-ionic.html" class="btn btn-default"><i class="glyphicon glyphicon-chevron-left"></i> 이전</a>
<a href="create-ionic-application.html" class="btn btn-default pull-right">다음 <i class="glyphicon 
glyphicon-chevron-right"></i></a>
</div>
</div>


