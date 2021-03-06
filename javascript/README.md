# 전역변수를 지양해야 하는 이유

# 전역 변수 === 시한폭탄
전역 변수에는 당연하게도 문제가 많은데, 크게 네 가지로 나눌 수가 있다.

### 1. 암묵적 결합
전역 변수는 이름 그대로 소스 코드 어디서든지 사용할 수 있는 변수다. 어느 위치의 어느 코드든지 전역 변수를 참조하고, 변경할 수 있다는 것이다. 이것을 암묵적 결합(Implicit coupling)이라고 하는데, 언뜻 듣기에는 편리하고 좋을 것 같은 느낌이 들기도 한다. 하지만, 전역 변수의 유효 범위 즉, 소스 ***코드의 길이가 길어질수록 가독성은 저하*** 되고, 의도치 않게 상태가 변경되는 등의 위험성이 있다.

### 2. 긴 생명 주기
앞서 말했지만, ***전역 변수의 생명 주기는 길다. 애플리케이션의 입장으로 보자면, 영원불멸의 삶을 사는 것이다. 그리고, 그에 따른 부작용은 고스란히 애플리케이션의 성능 저하***로 이어지게 된다.

이를테면, 소스 코드 내의 모든 함수들이 아무때나 참조하고, 상태를 변경할 수도 있는 24시간 편의점과 같다. 그렇기 때문에 메모리 리소스를 오랫동안 소비하는 것은 당연하다.

특히, var 키워드의 경우는 중복 선언까지 허용하는 만큼 언제 어디서 변수명이 변경될 지 모르는 일이다.

### 3. 스코프 체인 상에서 종점에 존재

전역 변수의 세 번째 문제점은 ***스코프 체인 상에서 가장 마지막에 존재*** 한다는 점이다. 이는 ***변수를 검색할 때 전역 변수가 가장 마지막에 검색된다는 말인데, 따라서 전역 변수의 검색 속도가 가장 느리다***는 말이기도 하다.

### 4. 네임 스페이스 오염

***자바스크립트의 단점 중 하나는 파일이 분리되어 있어도 하나의 전역 스코프를 공유*** 한다는 점이다. 그래서 별도의 파일이라고 해도 동일한 이름을 지닌 변수나 함수가 같은 스코프 내에 존재할 가능성이 있다는 것인데, 이것이 내 인생의 변수가 될 수도 있다.