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
<div v-bind: id=”rawId | formatId”></div>
```

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

## Vue Computed 속성
특정 데이터의 변경사항을 실시간 처리<br>
캐싱을 이용하여 데이터의 변경이 없을 경우 캐싱된 데이터 반환<br>
setter, getter를 직접 지정가능<br>
작성은 method 형태로 작성하지만 vue에서 proxy처리하여 property처럼 사용<br>

## Vue Watch 속성
Vue Instance의 특정 property가 변경될 때 실행할 콜백 함수 설정

## Vue event
Dom event를 청취하기 위해 v-on directive 또는 @ 사용<br>
inline event handling : 메소드 이름을 직접 바인딩 하는 대신 인라인 javascript 구문에 메소드를 사용할 수도 있다. 원본 DOM 이벤트에 엑세스 해야하는 경우 특별한 $event 변수를사용해 메소드에 전달 가능<br>
method를 이용한 event handling

## Event Modifier 
event.preventDefault() 와 같이 method내에 작업을 할 수도 있지만 method는 DOM의 이벤트를 처리하는 것보다 data 처리를 위한 로직으로만 작업하는 것이 좋다.<br>
이 문제를 해결하기위해 vue는 v-on이벤트에 이벤트 수식 제공<br>
- ```v-on.click.stop=”doThis”``` : 클릭 이벤트 전파 중단
- ```v-on:submit.prevent=”onSubmit”``` : 제출 이벤트가 페이지를 다시 로드하지 않음
- ```v-on:click.stop.prevent=”doThat”``` : 수식어는 체이닝 가능
- ```v-on:submit.prevent``` : 단순히 수식어만 사용 가능

## 키 수식어 ( Key Modifier ) 
- v-on:keyup.enter=”submit” : 엔터키를 땟을때 submit해라
- .enter( .13 )
- .tab
- .delete(delete와 backspace 키 모두 캡처)
- .esc
- .space
- .up
- .down
- .left
- .right

## ref, $refs
뷰에서는 $refs 속성을 이용해 DOM에 접근 가능<br>
하지만 Vue의 가장 중요한 목적 중 하나는 개발자가 DOM을 다루지 않게 하는 것이므로 되도록 ref를 사용하는 것을 피하는 것이 좋다.<br>
ex) ```<input type=”text” v-model=”id” ref=”id”>```

```console.log(this.$refs.id.value)``` => id 에 입력한 값 출력됨

## class binding
element의 class 와 style을 변경<br>
v-bind:class 는 조건에 따라 class 적용 가능

## form input bindings ( 폼 입력 바인딩)
v-model directive를 사용하여 폼 input과 textarea element에 양방향 데이터 바인딩 생성 가능<br>
text, textarea 태그는 value 속성과 input 이벤트<br>
체크박스, 라디오버튼은 checked 속성과 change 이벤트<br>
select 태그는 value를 prop으로 change 를 이벤트로 사용<br>

## form 수식어
.lazy : change 이벤트 이후 동기화 ```ex)v-model.lazy=”msg”```<br>
.number : 사용자 입력이 자동으로 숫자로 형 변환됨<br>
.trim : input에 입력한 값이 자동으로 trim<br>

## Component
Vue 의 가장 강력한 기능 중하나<br>
HTML Element를 확장하여 재사용 가능한 코드를 캡슐화<br>
Vue Component는 vue Instance이기도 하기 때문에 모든 옵션 객체를사용<br>
Life Cyfcle Hook 사용 가능<br>
전역 컴포넌트
```
Vue.component(‘my-component’,{
	//옵션
}
```
지역 컴포넌트 : 컴포넌트를 components 인스턴스 옵션으로 등록함으로써 다른 인스턴스, 컴포넌트 범위에서만 사용할 수 있는 컴포넌트를 만들 수 있음
```
new Vue({   // 
	components:{
	}
})
```

## 컴포넌트간 통신
부모에서 자식은 props라는 특별 속성으로만 전달가능<br>
자식에서 부모는 event로만 전달 가능<br>

## props 랜더링 과정
new Vue()로 상위 컴포넌트인 인스턴스를 하나 생성<br>
Vue.component()를 이용하여 하위 컴포넌트인 child-component 생성<br>
<div id=”app”> 내부에 <child-component>가 있기 때문에 하위 컴포넌트가 된다. 처음 생성한 인스턴스 객체가 #app의 요소를 가지기 때문에 부모자식관계 성립.<br>
```
하위 컴포넌트에 props 속성 정의[‘propsdata’]
html에 컴포넌트태그child-component 를 추가한다.
하위 컴포넌트에 v-bind속성을 사용하면 상위 컴포넌트의 data의 key에 접근 가능
상위 컴포넌트의 message 속성값인 STring 값이 하위 커모넌트의 props데이터로 전달된다.
하위 컴포넌트의 template 속성에 정의된 <span>{{propsdata}}</span>에 전달
```

## 동적 props
v-bind를 사용하여 부모의 데이터에 props를 동적으로 바인딩 가능
데이터가 상위에서 업데이트 될 떄마다 하위 데이터로 전달
```<child v-bind:my-message=”parentMsg”></chld>```

## 객체의 속성 전달 props
오브젝트의 모든 속성을 전달할 경우 v-bind:prop-name 대신 v-bind만 작성함으로써 모든 속성을 prop으로 전달 가능
```post : {
id:1,
title:’myjourney’
}
```
```
<blog-post v-bind=”post”></blog-post>
```
<br>
## 사용자 정의 이벤트
이벤트 이름:<br>
- 컴포넌트 및 props와는 달리 이벤트는 자동 대소문자 변환을 제공하지 않는다.<br>
- 대소문자를 혼용하는 대신에 emit할 정확한 이벤트 이름을 작성하는 것을 권장<br>
- v-on 이벤트 리스너는 항상 자동으로 소문자 변환되기 때문에 v-on:myEvent는 자동으로 v-on:myevent로 변환됨. 이름이 my-event일 경우 myevent이벤트를 들을 수 없음<br>
- 이러한 이유때문에 이벤트 이름에는 kebab-case 사용 권장<br>
이벤트 발생 : <br>
	```vm.$emit(“이벤트명”, [...파라미터]);```
이벤트 수신:<br>
```vm.$on(“이벤트명”, 콜백함수(){ } );```


## Event Bus
비 상하위간 통신<br>
비어있는 Vue Instance 객체를 Event Bus로 사용<br>
복잡해질 경우 상태관리 라이브러리인 Vuex 사용 권장<br>

## Axious
Vue에서 권고하는 HTTP 통신 라이브러리
```
axios({
	method: ‘get’,
	url: ‘/user/ssafy’,
	responseType: ‘json’,
})
.then(function ( response ) {
	//logic
})
```
## Vue-router 
라우팅 : 웹페이지 간의 이동 방법<br>
- vue.js의 공식 라우터
- 라우터는 컴포넌트와 맵핑
- Vue를 이용한 SPA를 제작할 때 유용
- URL에 따라 컴포넌트를 연결하고 설정된 컴포넌트를 보여줌
```
const router = new VueRouter({
	routes: [
		{path: ‘/’, component: Main // 라우트 컴포넌트 정의 },
		{path: ‘/’, component: Main // 라우트 컴포넌트 정의 },
	]
});
```

router 이동 및 렌더링<br>
네비게이션을 위해 route-link 컴포넌트 사용<br>
속성은 ‘to’ prop을 사용<br>
기본적으로는 <route-link>는 <a> 태그로 랜더링<br>
```ex) <router-link to=”/”> Home</router-link>```


## Vuex

- 상태관리 패턴 + 라이브러리
- 어플리케이션의 모든 컴포넌트에 대한 중앙 집중식 저장소 역할을 한다.
- 예측 가능한 방식으로 상태를 변경할 수 있다.
- 대형 규모의 웹 앱에서 컴포넌트 간의 데이터를 더 효율적으로 전달 가능

앱의 규모가 커지게되면 중간에 거쳐야 할 컴포넌트가 많아지거나 데이터 흐름을 파악하기 힘들다.

## 상태관리 패턴


