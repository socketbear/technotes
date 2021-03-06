JG Front End Framework set 소개
=====
JAVA 기반의 Back-End에서는 Spring Framework를 이용하여 MVC 형태로 구축할 수 있다.
대부분 개발자들은 MVC 모델에 대해 필요성을 잘 알고 있어서 이미 구조화되어 개발할 수 있는 Backend 쪽을 선호는 경향이 있다.
Front-End는 자신들이 알기로 구조화 되어 있지 않고, jQuery만 알면 개발할 수 있으며 중구난방으로 개발되는 것으로 알고 있다.
그래서, Front-End는 기술 자체 보다는 서비스를 구성하는 개발 난이도가 높다 생각한다.

jQuery 만을 사용하여 서버에서 API정보를 받고 View 출력화고 이벤트 처리를 할 때면 언제 어디서 어떤 소스가 접근하여 View가 변경되는지 알기 힘들다.
여기 저기에서 접근하여 변경하기 때문이다. 개발 시 구조화 되어 개발하지 않는다면 유지보수 난이도가 최악으로 치닫게 된다.
이를 해결하기 위해 클로저나 프라미즈 혹은 ECMA6 기법들을 활용하여 방법을 모색해 보지만 개발자마다 개발 스타일도 다르기 때문에 쉽지 않다.

하지만, 근래에 들어서 Front-End 쪽도 Back-End와 마찬가지로 구조화되는 기치가 나오고 있다.
특정 Framework를 활용하여 Back-End와 같이 이미 검증된 MVC 모델을 개발 간 차용하는 것이다.
물론 Front-End 구조 및 환경 상 Back-End와 동일하게 구성할 수 는 없지만 그와 유사하게 구성된 Framework들이 있다.

그 중 가장 대표적인 Framework는 Angularjs다.
구글에서 주도적으로 개발되고 있는 Angularjs는 MVC 모든 것을 표현 가능한 Framework이다.
하지만, 무겁다는 점과 IE9 이상부터 지원되기에 개발 환경 상 맞지않다.

또 하나로 대표할 수 있는 것은 Facebook의 Reactjs다.
특별하게도 Front-End에서는 View(개발과 수정)가 집중적이기 때문에 Reactjs 또한 View에 집중된 프레임워크다.
Controller와 Model 부분은 다른 라이브러리를 활용하여 구성하게 되어 있으며, 
이를 jQuery나 순수 Javascript를 정해진 규칙에 의거하여 구성하는 것이다.

물론 flux나, redux, reflux와 같이 Reactjs와 궁합이 맞는 MC 전용의 프레임워크들도 있지만, 이들은 모두 IE8에서 동작하지 않는다.

Reactjs의 장점은 가볍다는 것이다. View 전용이기 때문에 많은 것을 지원하는 Angularjs 보다 가볍다.
그리고, View를 Component와 시켜, 재사용성을 강조하는 방식을 강제적 개발하게 한다.
또한, 러닝 커브 (기술 습득 시 걸리는 시간 혹은 난이도) 가 다른 프레임워크에 비해 적다.

하지만, Reactjs 단점은 .jsx라는 새로운 확장자로 구성되고, 이는 컴파일을 통해 .js 항목으로 생성해야 한다.
개발자 입장에서는 귀찮고 힘든일이다. 하지만, 이런것들을 자동으로 인지하고 관리하는 모듈이 있다면 개발 속도나 편리성이 향상될 것이다.

그것이 바로 Webpack이다.

Webpack
-----
Webpack은 Task Runner라고 불리면서 배포를 제외한 배포만 하기 전까지 모든것들을 자동으로 구성해주는 툴이다.
Reactjs에서 만들어진 .jsx 만 컴파일 한다면 쓸 이유가 없다.
다른 매력적인 이유가 많기 때문에 이를 선정하였다.

첫번째로, 코드 합치기. Front-End 개발에는 태생적으로 많은 Javascript 소스가 들어가고, 많은 라이브러리를 쓸 수 밖에 없다.
서비스 사용자가 웹 페이지를 접근하여 서비스를 사용하려면 개발 간 사용된 javascript를 다운 받아야 하는데, 많은 개수의 파일을 가져오는 것 보다 한개의 파일을 가져오는 것이 빠르다는 것이다.

두번째로, 코드 난독화. javascript 소스는 서비스 사용자가 열람 시 사용하는 웹브라우져에서 F12 만 누르면 바로 볼 수 있다.
즉, 보안에 취약한데, 이를 쉽게 볼 수 없도록 소스들을 변형 시킨다.

세번째로, 코드 압축. javascript 소스에 필요없는 것들 (예를 들어 \n) 모두 정리하여 한줄로 만들어 버린다.

네번째로, Front-End 전용 웹 서버. 이전에는 서버 통신 개발을 위해서 Front-End 개발자도 이클립스를 설치하고 서버 소스를 다운받아서, 컴파일하고 이를 localhost에 서버로 올려 사용했어야만 했다.
그럴 필요 없이, 자체적으로 웹 서버를 구성하여 개발한 웹 페이지를 확인할 수 있다. 
서버 통신이 필요한 경우 개발 서버로 API등을 붙여서 사용가능하며, 이때 Proxy 기능을 사용하여 Cross domain 오류를 우회할 수 있게 지원한다.

다섯번째로, Hot loader. 웹 소스를 변경하고 확인하려면, 웹 브라우져에서 새로고침으로 봐야 확인 할 수 있다.
Webpack은 Hot loader를 지원하면서 소스 변경을 저장하자 마자, 이를 감지하고 변경한 부분을 컴파일까지 자동적으로 수행된다.
또한, 전용 웹 서버가 웹 브라우져와 소켓통신을 하면서 변경된 부분을 바로 적용해 준다.
즉, 새로 고침 없어도 개발자 눈에 바로 확인이 가능하다.

이런한 이유로, Webpack을 사용하면 귀찮고 힘든 작업을 바로 해주는 환경을 구성하기 때문에 컴포넌트화된 소스를 운영자에게 인계할 때 큰 교육없이 알려줄 수 있다.

Report 출력
-----
Report를 웹 페이지에 구성하기 위해서 선택한 라이브러리는 echart이다.
IE8에서 동작하는 차트 라이브러리는 거의 없다. 대부분 IE9 이상만 지원하며 IE8 이하는 대부분 유료만 존재한다. (그것도 비싸다!)
하지만, Echart는 IE7부터 지원하며 많은 수의 차트를 표현할 수 있는 오픈 소스이다.

그리고, 웹페이지로 구성된 화면을 출력하기 위해 Phantomjs를 사용한다.
Phantomjs는 가상의 웹 브라우저를 사용하여 그 안에 출력된 페이지를 이미지 혹은 PDF로 출력하게 한다.

Socket IO
-----
장기간의 호출 간 Callback을 처리를 어떻게 해야할까?
20초 걸리는 작업이 있다고 할 때, 웹 상에서 호출 시, API를 계속 물고 있다면 사용자 입장에서는 보기 좋지 못하다.
요청 이후에도 다른 작업을 할 수 있고, 서버에서 작업이 끝날 때 따로 알림을 줄 수 있는 구조가 된다면 보기 좋을 것이다.
이를 Socket IO를 통하여 처리 할 수 있다.

서버의 작업은 기본적으로 (특정 API 혹은 전체) Background 작업을 하면서 예외처리에 부합되는 3초 이상 넘어가는 작업이 발생 시, 소켓으로 Callback 받아 처리할 수 있도록 하는 방법을 구성할 수 있다.

기타
-----
Webpack은 개발자 머신에서 동작되어 개발 시 도움을 주는 툴이라면, phantomjs나 socketio는 nodejs 기반으로 동작하는 유틸리티다.
이는 WEB 서버 내에서 동작하며, Nodejs를 서버가 아닌 phantomjs나 socketio를 사용할 목적이므로 따로 소프트웨어 구성도에 넣지 않았다.
참고로 Spring은 개발 시 전천후로 사용하기 때문에 소프트웨어 구성도에 넣었다.