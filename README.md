# visitorbook

Vue.js + firebase를 이용하여 만든 방명록

[이곳](https://wonyoungyun.github.io/visitor-book/)에서 완성된 결과물을 확인 할 수 있습니다.

## Project setup

```
npm install
```

### Compiles and hot-reloads for development

```
npm run serve
```

### Compiles and minifies for production

```
npm run build
```

## details

firebase 사용을 위해 설치

```
npm install --save firebase
```

vue와 firebase 데이터 바인딩을 위한

```
npm install --save vuefire
```

해당 명령어를 통해 vuefire와 firebase를 설치한다.

```
import VueFire from "vuefire";
import firebase from "firebase";

Vue.use(firebase);
Vue.use(VueFire);
```

를 통해 vuefire와 firebase를 Vue에 등록한다.

```
const config = {
apiKey: ""
authDomain: ""
databaseURL: ""
projectId: ""
storageBucket: ""
messagingSenderId: ""
};
```

firebase의 apiKey와 정보가 있는 config를

```
firebase.initializeApp(config);
```

을 통해 firebase와 연결

```
<template>
    <div v-for="(item,index) in Coments" :key="index" class="user-area">
</template>

<script>
...

firebase: {
Coments: comentsRef
},

...
</script>
```

vuefire로 Vue에 firebase의 데이터를 바인딩 할 수 있다.

```
const comentsRef = firebase.database().ref(`Coments`);
```

를 통해 firebase에 미리 만든 Coments테이블에 접근하여

AddComent 컴포넌트에서 받은 데이터를 VisitorBook에서 firebase의 Coments에 저장한다.

각각의 데이터에는 키가 자동으로 할당이 되며

```
comentsRef.child(user[".key"]).remove();
```

그 키로 데이터를 제거 할 수 있다.

## 느낀점

firebase의 사용법이 잘되 있어서 적용하기도 쉽고 이용하는 것 자체도 어렵지 않았다.

firebase의 실시간 데이터 베이스를 이용하여, 실시간으로 데이터를 저장하고 삭제하는 것을 통해
간단한 프로젝트를 위한 백엔드로 사용하도 괜찮다고 생각했다.

firebase는 주로 인증서비스 구현을 위해 많이 사용한다고 들었는데 그런 인증서비스도 한번 구현해 보고 싶다.
