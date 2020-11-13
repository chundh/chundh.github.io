---
layout: post
title:  "MVC, MVP, MVVM"
categories: [Class, Computer_Science]
---

### 디자인 패턴의 탄생
- 규모가 작은 프로젝트에서는 입력, 출력, 데이터 연산부분이 구별되지 않아도 큰 무리가 없었다.
- 하지만 규모가 커질수록 코드의 양이 많아지고, 이를 기능별로 분류하지 않는다면 코드가 뒤섞여서 코드의 재사용성이 떨어지고, 개발 효율도 나빠진다.
- 그래서 크게 기능별로 단위를 구성하여 개발하는 패턴이 많이 도입되고 있다.

### MVC
- Model, View, Controller로 구성되어 있다.
- Model: 실질적으로 데이터 처리가 이루어지는 공간이다. Controller로 부터 데이터의 변화를 받고, 업데이트된 데이터를 보내준다. 다른 모듈에 의존성을 갖지 않으므로 재사용이 가능하다.
- View: 실질적으로 사용자에게 보여지는 UI가 배치되는 곳이다. Controller로 부터 받은 데이터를 화면으로 보여준다. 안드로이드에서는 .xml이 해당된다.
- Controller: 사용자의 입력에 반응하여 데이터를 처리한다. Model에서 업데이트된 데이터를 받고, View로 데이터를 뿌려주어 갱신된 화면을 사용자에게 제공한다. 안드로이드에서는 Activity나 Fragment가 해당된다.
- 문제점:
  - View와 Controller가 강하게 연결되어있다.
  - 각 모듈의 분리를 위해서 서로서로 의존성을 낮춰야 하지만 안드로이드의 특성상 Controller가 View에 관여해 직접 데이터를 구성해야한다.
  - 설계상 Activity와 Fragment에 많은 양의 코드가 집중된다.

### MVP
- Model, View, Presenter로 구성되어 있다.
- Model: 위와 동일하다
- View: MVC모델에서 Controller가 담당하던 Activity와 Fragment의 내용이 넘어왔다. 직접 화면을 구성하여 의존성을 낮췄다. 그리고 View를 관리하는 interface를 상속하는 클래스를 인스턴스로 가져 Presenter를 독립적으로 만든다.
- Presenter: 단순한 interface이다. Controller와 비슷한 사용자의 입력에 반응하는 역할을 Abstract Method의 구현으로 하지만, View와 강하게 연결되어있지 않다는 점에서 차이가 있다.
- 문제점: 각 View마다 Presenter 인스턴스를 각자 갖고 있다. 그렇기 때문에 n개의 View가 있다면 비슷한 동작을 하는 Presenter가 n개가 생성된다.

### MVVM
- Model, View, ViewModel로 구성되어 있다.
- Model: 위와 동일하다.
- View:
- ViewModel: 