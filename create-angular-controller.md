---
layout: module
title: 제 5장&#58; 세션 컨트롤러 생성하기
---
<!--
[AngularJS controllers](https://docs.angularjs.org/guide/controller) act as the glue between views and services. A controller often invokes a method in a service to get data that it stores in a [scope](https://docs.angularjs.org/guide/scope) variable so that it can be displayed by the view. In this module, you create two controllers: SessionsCtrl manages the session list view, 
and SessionCtrl manages the session details view.

## Step 1: Declare starter.services as a Dependency

The two controllers you create in this module use the **Session** service defined in the starter.services module. To 
add 
starter.services as a dependency to the starter.controller module: 

1. Open **conference/www/js/controllers.js**

1. Add **starter.services** as a dependency to make the Session service available to the controllers:

    ```
    angular.module('starter.controllers', ['starter.services'])
    ```

## Step 2: Implement the Session List Controller

1. In controllers.js, delete **PlayListsCtrl** (plural)

1. Replace it with a controller named **SessionsCtrl** that retrieves the list of conference sessions using the Session 
service and stores it in a scope variable named **sessions**:

    ```
    .controller('SessionsCtrl', function($scope, Session) {
        $scope.sessions = Session.query();
    })
    ```

## Step 3: Implement the Session Details 컨트롤러 구현

1. In controllers.js, delete **PlayListCtrl** (singular)
 
1. Replace it with a controller named **SessionCtrl** that retrieves a specific session using the Session service and 
stores it in a scope variable named **session**:

    ```
    .controller('SessionCtrl', function($scope, $stateParams, Session) {
        $scope.session = Session.get({sessionId: $stateParams.sessionId});
    });
    
    ```
-->

[AngularJS 컨트롤러](https://docs.angularjs.org/guide/controller)는 뷰와 서비스 사이에서 접착제처럼 동작합니다. 컨트롤러는 종종 [스코프](https://docs.angularjs.org/guide/scope) 변수에 저장된 데이터를 가져오기위해 서비스에서 메소드를 동작시켜 뷰에서 보여줍니다. 이번 장에서 두개의 컨트롤러를 생성합니다: SessionsCtrl은 세션 리스트 뷰를 관리하고, SessionsCtrl은 세션 디테일 뷰를 관리합니다.

## 1단계: 종속으로써 starter.services를 선언

1. **conference/www/js/controllers.js**을 엽니다.

1. 세션 서비스가 가능하기 위해 컨트롤러에 종속으로써 **starter.services**를 추가합니다.

    ```
    angular.module('starter.controllers', ['starter.services'])
    ```

## 2단계: Session List 컨트롤러 구현

1. controllers.js에서, **PlayListsCtrl**(복수)을 삭제합니다.

1. 세션 서비스를 사용하여 회의 세션의 목록을 검색하는 **SessionsCtrl** 컨트롤러를 **sessions** 스코프 변수에 저장하도록 수정합니다:

    ```
    .controller('SessionsCtrl', function($scope, Session) {
        $scope.sessions = Session.query();
    })
    ```

## 3단계: Session Details 컨트롤러 구현

1. controllers.js에서 **PlayListCtrl**(단수)을 삭제합니다.

1. 세션 서비스를 이용하여 특정한 세션을 검색하는 **SessionCtrl** 컨트롤러를 **session** 스코프 변수에 저장하도록 수정합니다:

    ```
    .controller('SessionCtrl', function($scope, $stateParams, Session) {
        $scope.session = Session.get({sessionId: $stateParams.sessionId});
    });
    
    ```



<div class="row" style="margin-top:40px;">
<div class="col-sm-12">
<a href="create-angular-service.html" class="btn btn-default"><i class="glyphicon glyphicon-chevron-left"></i> 
이전</a>
<a href="create-ionic-template.html" class="btn btn-default pull-right">다음 <i class="glyphicon 
glyphicon-chevron-right"></i></a>
</div>
</div>


