# VueJs 정리

## Vue.js란?
컴포넌트(Component) 기반의 SPA(Single Page Application)를 구축할 수 있게 해주는 프레임워크이다.<br>
컴포넌트는 각 UI 요소들이라고 생각하면 된다.<br>
SPA는 한개의 페이지 안에서 필요한 영역 부분만 로딩시키는 방법으로 빠른  페이지 변환이 가능하지만 최초 실행 시 로딩이 길다.


## Vue.js의 특징
- Approachable(접근성)
- Versatile(유연성)
- Performant(고성능)

## MVVM 패턴
- Model + View + ViewModel
- Model : 순수 자바스크립트 객체
- View : 웹 페이지의 DOM
- ViewModel : Vue의 역할. -> 기존에는 자바스크립트로 view에 해당하는 DOM에 접근하거나 수정하기 위해 jQuery 같은 라이브러리를 이용했지만 Vue는 view와 Model을 연결하고 자동으로 바인딩 하므로 양방향 통신이 가능하다.



