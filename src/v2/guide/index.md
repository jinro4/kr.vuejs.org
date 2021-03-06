---
title: 시작하기
type: guide
order: 2
---

## Vue.js가 무엇인가요?

Vue(/vjuː/ 로 발음, **view** 와 발음이 같습니다.)는 사용자 인터페이스를 만들기 위한 **진보적인 프레임워크** 입니다. 다른 단일형 프레임워크와 달리 Vue는 점진적으로 채택할 수 있도록 설계하였습니다. 핵심 라이브러리는 뷰 레이어만 초점을 맞추어 다른 라이브러리나 기존 프로젝트와의 통합이 매우 쉽습니다. 그리고 Vue는 [현대적 도구](single-file-components.html) 및 [지원하는 라이브러리](https://github.com/vuejs/awesome-vue#libraries--plugins)와 함께 사용한다면 정교한 단일 페이지 응용프로그램을 완벽하게 지원할 수 있습니다.

숙련된 프론트엔드 개발자이고 Vue를 다른 라이브러리/프레임워크와 비교하고 싶다면 [다른 프레임워크와의 비교](comparison.html)를 확인하십시오.

## 시작하기

<p class="tip">공식 가이드는 HTML, CSS 및 JavaScript에 대한 중간 수준의 지식을 전제로 합니다. 프론트 엔드 개발에 완전히 익숙하지 않다면 를 시작하는 첫 번째 단계로 시작하는 것은 좋은 생각이 아닙니다. 기본을 파악한 다음 다시 해보세요! 다른 프레임워크에 대한 사전 경험이 도움이 되지만 필수는 아닙니다.</p>

Vue.js를 시험해 볼 수있는 가장 쉬운 방법은 [JSFiddle Hello World 예제](https://jsfiddle.net/chrisvfritz/50wL7mdz/)을 사용하는 것입니다. 다른 탭에서 자유롭게 열어 본 후 몇 가지 기본 예제를 따라 가십시오. 또는 단순히 `.html` 파일을 만들고 Vue를 다음과 같이 포함시킬 수 있습니다.

``` html
<script src="https://unpkg.com/vue/dist/vue.js"></script>
```

[설치](installation.html) 페이지에는 Vue 옵션이 추가로 제공됩니다. Node.js 기반 빌드 도구에 아직 익숙하지 않으면 `vue-cli`로 시작하는 것을 추천하지 **않습니다.**

## 선언적 렌더링

Vue.js의 핵심은 간단한 템플릿 구문을 사용해 선언적으로 DOM에 데이터를 렌더링 하는 것 입니다.

``` html
<div id="app">
  {{ message }}
</div>
```
``` js
var app = new Vue({
  el: '#app',
  data: {
    message: '안녕하세요 Vue!'
  }
})
```
{% raw %}
<div id="app" class="demo">
  {{ message }}
</div>
<script>
var app = new Vue({
  el: '#app',
  data: {
    message: '안녕하세요 Vue!'
  }
})
</script>
{% endraw %}

우리는 이미 첫 Vue 앱을 만들었습니다! 문자열 템플릿을 렌더링 하는 것과 매우 유사하지만 사실 Vue는 더 많은 작업을 합니다. 데이터와 DOM이 연결되어 이제 모든 것이 **반응형** 입니다. 어떻게 알 수 있을까요? 브라우저의 JavaScript 콘솔을 열고 `app.message`를 다른 값으로 설정해 보십시오. 그에 따라 렌더링 된 예제를 볼 수 있습니다.

텍스트 보간 이외에도 다음과 같은 엘리먼트 속성을 바인딩 할 수 있습니다.

``` html
<div id="app-2">
  <span v-bind:title="message">
    내 위에 마우스를 올리면 동적으로 바인딩 된 title을 볼 수 있습니다!
  </span>
</div>
```
``` js
var app2 = new Vue({
  el: '#app-2',
  data: {
    message: '이 페이지는 ' + new Date() + ' 에 로드 되었습니다'
  }
})
```
{% raw %}
<div id="app-2" class="demo">
  <span v-bind:title="message">
    내 위에 마우스를 올리면 동적으로 바인딩 된 title을 볼 수 있습니다!
  </span>
</div>
<script>
var app2 = new Vue({
  el: '#app-2',
  data: {
    message: '이 페이지는 ' + new Date() + '에 로드 되었습니다'
  }
})
</script>
{% endraw %}

여기서 우리는 새로운 곳에 다다랐습니다. `v-bind` 속성은 **지시문** 이라고 합니다. 지시문은 Vue에서 제공하는 특수 속성임을 나타내는 `v-` 접두어가 붙어있으며 사용자가 짐작할 수 있듯 렌더링 된 DOM에 특수한 반응형 동작을 합니다. 기본적으로 "이 요소의 `title` 속성을 Vue 인스턴스의 `message` 속성으로 최신 상태를 유지 합니다."

JavaScript 콘솔을 다시 열고 `app2.message = '새로운 메시지'` 라고 입력하면 HTML(이 경우에 `title` 속성)이 업데이트 되었음을 다시 한번 확인할 수 있습니다.

## 조건문과 반복문

엘리먼트의 존재여부를 토글하는 것은 아주 간단합니다.

``` html
<div id="app-3">
  <p v-if="seen">이제 나를 볼 수 있어요</p>
</div>
```

``` js
var app3 = new Vue({
  el: '#app-3',
  data: {
    seen: true
  }
})
```

{% raw %}
<div id="app-3" class="demo">
  <span v-if="seen">이제 나를 볼 수 있어요</span>
</div>
<script>
var app3 = new Vue({
  el: '#app-3',
  data: {
    seen: true
  }
})
</script>
{% endraw %}

계속해서, `app3.seen = false` 를 콘솔에 입력하세요. 메시지가 사라지는 것을 확인해야 합니다.

이 예제는 텍스트와 속성뿐 아니라 DOM의 **구조** 에도 데이터를 바인딩 할 수 있음을 보여줍니다. 또한 Vue 엘리먼트가 Vue에 삽입/갱신/제거 될 때 자동으로 [전환 효과](transitions.html)를 적용할 수 있는 강력한 시스템을 제공합니다.

몇가지 지시문이 있습니다. 각 지시문마다 고유한 기능이 있습니다. 예를 들어 `v-for` 지시문은 배열의 데이터를 사용해 항목 목록을 표시하는데 사용할 수 있습니다.

``` html
<div id="app-4">
  <ol>
    <li v-for="todo in todos">
      {{ todo.text }}
    </li>
  </ol>
</div>
```
``` js
var app4 = new Vue({
  el: '#app-4',
  data: {
    todos: [
      { text: 'JavaScript 배우기' },
      { text: 'Vue 배우기' },
      { text: '무언가 멋진 것을 만들기' }
    ]
  }
})
```
{% raw %}
<div id="app-4" class="demo">
  <ol>
    <li v-for="todo in todos">
      {{ todo.text }}
    </li>
  </ol>
</div>
<script>
var app4 = new Vue({
  el: '#app-4',
  data: {
    todos: [
      { text: 'JavaScript 배우기' },
      { text: 'Vue 배우기' },
      { text: '무언가 멋진 것을 만들기' }
    ]
  }
})
</script>
{% endraw %}

콘솔에서, `app4.todos.push({ text: 'New item' })`을 입력하십시오. 목록에 새 항목이 추가되어야 합니다.

## 사용자 입력 핸들링

사용자가 앱과 상호 작용할 수 있게 하기 위해 우리는`v-on` 지시문을 사용하여 Vue 인스턴스에 메소드를 호출하는 이벤트 리스너를 첨부 할 수 있습니다 :

``` html
<div id="app-5">
  <p>{{ message }}</p>
  <button v-on:click="reverseMessage">메시지 뒤집기</button>
</div>
```
``` js
var app5 = new Vue({
  el: '#app-5',
  data: {
    message: '안녕하세요! Vue.js!'
  },
  methods: {
    reverseMessage: function () {
      this.message = this.message.split('').reverse().join('')
    }
  }
})
```
{% raw %}
<div id="app-5" class="demo">
  <p>{{ message }}</p>
  <button v-on:click="reverseMessage">메시지 뒤집기</button>
</div>
<script>
var app5 = new Vue({
  el: '#app-5',
  data: {
    message: '안녕하세요! Vue.js!'
  },
  methods: {
    reverseMessage: function () {
      this.message = this.message.split('').reverse().join('')
    }
  }
})
</script>
{% endraw %}

이 메소드에서 우리는 단순히 DOM을 건드리지 않고 앱의 상태를 업데이트 합니다. 모든 DOM 조작은 Vue에 의해 처리되며 작성한 코드는 기본 로직에만 초점을 맞춥니다.

Vue는 또한 양식에 대한 입력과 앱 상태를 양방향으로 바인딩하는 `v-model` 지시문을 제공합니다.

``` html
<div id="app-6">
  <p>{{ message }}</p>
  <input v-model="message">
</div>
```
``` js
var app6 = new Vue({
  el: '#app-6',
  data: {
    message: '안녕하세요 Vue!'
  }
})
```
{% raw %}
<div id="app-6" class="demo">
  <p>{{ message }}</p>
  <input v-model="message">
</div>
<script>
var app6 = new Vue({
  el: '#app-6',
  data: {
    message: '안녕하세요 Vue!'
  }
})
</script>
{% endraw %}

## 컴포넌트를 사용한 작성방법

컴포넌트 시스템은 Vue의 또 다른 중요한 개념입니다. 이는 작고 그 자체로 제 기능을 하며 재사용할 수 있는 컴포넌트로 구성된 대규모 응용 프로그램을 구축할 수 있게 해주는 추상적 개념입니다. 생각해보면 거의 모든 유형의 응용 프로그램 인터페이스를 컴포넌트 트리로 추상화 할 수 있습니다.

![컴포넌트 트리](/images/components.png)

Vue에서, 컴포넌트는 본질적으로 미리 정의된 옵션을 가진 Vue 인스턴스 입니다. Vue에 컴포넌트를 등록하는 것은 간단합니다.

``` js
// todo-item 이름을 가진 컴포넌트를 정의합니다
Vue.component('todo-item', {
  template: '<li>할일입니다.</li>'
})
```

이제 다른 컴포넌트의 템플릿에서 사용할 수 있습니다.

``` html
<ol>
  <!-- todo-item 컴포넌트의 인스턴스 만들기 -->
  <todo-item></todo-item>
</ol>
```

그러나 이는 모든 할일에 대해 동일한 인스턴스를 렌더링 합니다. 부모 범위의 데이터를 하위 컴포넌트로 전달할 수 있어야 합니다. [prop](components.html#Props)을 허용하도록 컴포넌트 정의를 수정 해 보겠습니다.

``` js
Vue.component('todo-item', {
  // 이제 todo-item 컴포넌트는 사용자 정의 속성과 같은
  // "prop"를 허용합니다. 이 prop는 todo라고 합니다.
  props: ['todo'],
  template: '<li>{{ todo.text }}</li>'
})
```

이제 todo를 `v-bind`를 사용하여 반복된 각 컴포넌트에 전달할 수 있습니다.

``` html
<div id="app-7">
  <ol>
    <!-- 각 todo-item 에 todo 객체를 제공합니다. -->
    <!-- 그것의 컨텐츠는 동적입니다. -->
    <todo-item v-for="item in groceryList" v-bind:todo="item"></todo-item>
  </ol>
</div>
```
``` js
Vue.component('todo-item', {
  props: ['todo'],
  template: '<li>{{ todo.text }}</li>'
})

var app7 = new Vue({
  el: '#app-7',
  data: {
    groceryList: [
      { text: '채소' },
      { text: '치즈' },
      { text: '사람이 먹을 수 있는 무엇이든' }
    ]
  }
})
```
{% raw %}
<div id="app-7" class="demo">
  <ol>
    <todo-item v-for="item in groceryList" v-bind:todo="item"></todo-item>
  </ol>
</div>
<script>
Vue.component('todo-item', {
  props: ['todo'],
  template: '<li>{{ todo.text }}</li>'
})
var app7 = new Vue({
  el: '#app-7',
  data: {
    groceryList: [
      { text: '채소' },
      { text: '치즈' },
      { text: '사람이 먹을 수 있는 무엇이든' }
    ]
  }
})
</script>
{% endraw %}

이것은 예시를 위한 예제 입니다. 하지만 우리는 앱을 두개의 더 작은 단위로 나눌 수 있었고 자식은 부모로부터 prop 인터페이스를 통해 합리적으로 잘 분리하였습니다. 부모 앱에 영향을 주지 않으면서 더 복잡한 템플릿과 로직으로 `<todo-item>` 컴포넌트를 더욱 향상시킬 수 있습니다.

대규모 응용 프로그램에서는 개발을 쉽게 관리할 수 있도록 전체 앱을 컴포넌트로 나누어야 합니다. [나중에 이 가이드](components.html)에서 컴포넌트에 대해 더 많은 이야기를 나누겠습니다. 하지만 여기서는 컴포넌트로 앱의 템플릿이 어떻게 표시되는지에 대한 예를 보겠습니다.

``` html
<div id="app">
  <app-nav></app-nav>
  <app-view>
    <app-sidebar></app-sidebar>
    <app-content></app-content>
  </app-view>
</div>
```

### 사용자 정의 엘리먼트와의 관계

Vue 컴포넌트는 [Web Components Spec](http://www.w3.org/wiki/WebComponents/)의 일부인 **사용자 지정 엘리먼트** 와 매우 유사하다는 것을 눈치 챘을 수 있습니다. Vue의 컴포넌트 구문은 스펙 이후 느슨하게 모델링 되었기 때문입니다. 예를 들어 Vue 컴포넌트는 [Slot API](https://github.com/w3c/webcomponents/blob/gh-pages/proposals/Slots-Proposal.md)와 `is` 특수 속성을 구현합니다. 그러나 몇가지 중요한 차이가 있습니다.

1. Web Components Spec은 여전히 초안이며 모든 브라우저에서 기본적으로 구현되지 않습니다. 이에 비해 Vue 컴포넌트는 지원되는 모든 브라우저 (IE 9 이상)에서 폴리필을 필요로 하지 않으며 일관되게 작동합니다. 필요한 경우 Vue 컴포넌트는 기본 사용자 정의 엘리먼트 내에 래핑할 수 있습니다.

2. Vue 컴포넌트는 일반 사용자 정의 엘리먼트에서 사용할 수 없는 중요한 기능을 제공합니다. 특히 컴포넌트 데이터 흐름, 사용자 지정 이벤트 통신 및 빌드 도구 통합이 중요합니다.

## 더 해야할 것은 무엇인가요?

우리는 Vue.js 코어의 가장 기본적인 기능을 간략하게 소개했습니다. 이 가이드의 나머지 부분에서 더 자세한 세부 내용이 포함된 다른 고급 기능에 대해 다룰 예정이므로 꼭 읽어보시기 바랍니다.
