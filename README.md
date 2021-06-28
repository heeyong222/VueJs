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

## Vue Instance 생성
```
<script>
	new Vue({
		el:’#app’,
		data:{
			message: ‘1’
		}
	})
<script>
```
- el : Vue가 적용될 요소 지정. CSS Selector or HTML Element
- data : Vue에 사용되는 정보 저장. 객체 또는 함수의 2가지 형태가 있음
- template : 화면에 표시할 HTML, CSS 등의 마크업 요소를 정의하는 속성. 뷰의 데이터 및 기타 속성들도 함께 화면에 그릴 수 있다.
- methods : 화면 로직 제어와 관계된 method를 정의하는 속성. 마우스 클릭 이벤트 처리와 같이 화면의 전반적인 이벤트와 화면 동작과 관련된 로직을 추가.
- created : 뷰 인스턴스가 생성되자마자 실행할 로직 정의

## Vue Instance의 유효 범위
vue instance를 생성하면 html의 특정 범위 안에만 옵션속성들이 적용된다. 이것은 el 속성과 밀접한 관계가 있다.
1. 뷰 라이브러리 파일 로딩
2. 인스턴스 객체 생성(옵션 속성 포함)
3. 특정 화면 요소에 인스턴스를 붙임
4. 인스턴스 내용이 화면 요소로 변환
5. 변환된 화면 요소를 사용자가 최종 확인



