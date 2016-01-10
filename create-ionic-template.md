---
layout: module
title: 제 6장&#58; 템플릿 생성하기
---
<!--
In this module, you create two templates: sessions.html to display a list of sessions, and session.html to display the details of a particular session.

## Step 1: Create the sessions template

1. In the **conference/www/templates directory**, rename playlists.html (plural) to **sessions.html**

1. Implement the template as follows:

    ```
    {% raw %}
    <ion-view view-title="Sessions">
      <ion-content>
        <ion-list>
          <ion-item ng-repeat="session in sessions"
                    href="#/app/sessions/{{session.id}}">{{session.title}}</ion-item>
        </ion-list>
      </ion-content>
    </ion-view>
    {% endraw %}
    ```

    > Notice the use of the ng-repeat directive to display the list of sessions


## Step 2: Create the session template

1. Rename playlist.html (singular) to **session.html**
 
1. Implement the template as follows:
-->

이번 장에서 세션 목록을 보여주는 sessions.html과 특정한 세션의 자세한 내용을 보여주는 session.html, 두개의 템플릿을 생성합니다.

## 1단계: sessions 템플릿을 생성합니다.

1. **conference/www/templates directory**에서 playlists.html(복수)를 **sessions.html**으로 이름을 변경합니다.

1. 템플릿을 다음과 같이 구현합니다:

    ```
    {% raw %}
    <ion-view view-title="Sessions">
      <ion-content>
        <ion-list>
          <ion-item ng-repeat="session in sessions"
                    href="#/app/sessions/{{session.id}}">{{session.title}}</ion-item>
        </ion-list>
      </ion-content>
    </ion-view>
    {% endraw %}
    ```

    > 세션 목록을 보여주기 위해서 ng-repeat 디렉티브를 사용합니다.


## 2단계: session 템플릿을 생성합니다.

1. playlist.html(단수)를 **session.html**으로 이름을 변경합니다.
 
1. 다음과 같이 템플릿을 구현합니다:

    ```
    {% raw %}
    <ion-view view-title="Session">
      <ion-content>
        <div class="list card">
          <div class="item">
            <h3>{{session.time}}</h3>
            <h2>{{session.title}}</h2>
            <p>{{session.speaker}}</p>
          </div>
          <div class="item item-body">
            <p>{{session.description}}</p>
          </div>
          <div class="item tabs tabs-secondary tabs-icon-left">
            <a class="tab-item">
              <i class="icon ion-thumbsup"></i>
              Like
            </a>
            <a class="tab-item">
              <i class="icon ion-chatbox"></i>
              Comment
            </a>
            <a class="tab-item">
              <i class="icon ion-share"></i>
              Share
            </a>
          </div>
        </div>
      </ion-content>
    </ion-view>
    {% endraw %}
    ```
  
<div class="row" style="margin-top:40px;">
<div class="col-sm-12">
<a href="create-angular-controller.html" class="btn btn-default"><i class="glyphicon glyphicon-chevron-left"></i> 
이전</a>
<a href="angular-ui-router.html" class="btn btn-default pull-right">다음 <i class="glyphicon 
glyphicon-chevron-right"></i></a>
</div>
</div>


