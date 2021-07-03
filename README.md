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



## Vue Instance Life Cycle
- beforeCreate : Vue Instnace가 생성되고 각 정보의 설정 ㅈ언에 호출. DOM과 같은 화면 요소에 접근 불가능
- created : Vue Instance가 생성된 후 데이터들의 설정이 완료된 후 호출. Instance가 화면에 부착하기 전이기 때문에 template 속성에 정의된 DOM 요소에는 접근 불가
- beforeMount : 마운트가 시작되기 전에 호출
- mounted : 지정된 element에 Vue Instance 데이터가 마운트(부착) 된 후에 호출. Template 속성에 정의한 화면 요소에 접근할 수 있어 화면 요소를 제어하는 로직 수행
- beforeUpdate : 데이터가 변경될 때 virtual DOm이 랜더링. 패치되기 전에 호출
- updated : Vue에서 관리되는 데이터가 변경되어 DOM이 업데이트 된 상태. 데이터 변경 후 화면 요소 제어와 관련된 로직 추가
- beforeDestroy : Vue Instance가 제거되기 전에 호출
- destroyed : Vue Instance가 제거된 후에 호출

## 보간법(Interpolation)
{{ 속성명 }} 형식<br>
v-once를 사용하면 데이터 변경 시 업데이트 되지 않는 일회성 보간 수행

## 원시 HTML
이중 중괄호는 HTML이 아닌 일반 텍스트로 해석된다.<br>
HTML 을 출력하기 위해서는 v-html 디렉티브 사용
ex) ```<span v-html=”aaa”></span>```

## 바인딩
바인딩에는 한가지 표현식만 포함될 수 있으므로<br>
{{ var a = 1 }} 또는 // 구문. 표현식이아님<br>
{{ if( ok) {return msg} }} // 조건문은 작동x 삼항연산자 사용해야됨<br>
들은 작동하지 않는다. 

## 디렉티브
- v-model : 양방향 바인딩 처리를 위해서 사용(form 의 input, textarea)<br>
- v-bind : 엘리먼트의 속성과 바인딩 처리를 위해서 사용, 약어로 : 사용가능<br>
- v-show : 조건에 따라 엘리먼트를 화면에 랜더링. style의 display를 변경<br>
- v-if, v-else-if, v-else : 조건에 따라 엘리먼트를 화면에 렌더링<br>
ex)``` <span v-if=”age < 10”> ```<br>
- v-for : 배열이나 객체의 반복에 사용<br>
ex) ```v-for=”요소변수이름 in 배열” or   v-for=”(요소변수이름, 인덱스) in 배열”```<br>
- template : 여러 태그를 묶어서 처리할 경우 사용, v-if, v-for, component 등과 함께 많이 사용<br>
- v-cloak : Vue Instance가 준비될 때 까지 mustache 바인딩을 숨기는데 사용<br>



## Vue Filter

filter를 이용하여 표현식에 새로운 결과 형식 적용<br>
중괄호 보간법 또는 v-bind 속성에서 사용 가능<br>
ex) 
```{{ msg | upper }}
<div v-bind: id=”rawId | formatId”></div>```

전역 필터 : 
```
Vue.filter(
~~~~
)
```
지역 필터 : 
```
new Vue({
	el: ‘#app’,
	filters: {
		count2(a,b){
		~~
		}

})
```
