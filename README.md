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

```
npm install --save firebase
```

firebase 사용을 위해 설치합니다.

```
npm install --save vuefire
```

vue와 firebase의 데이터바인딩을 지원하는 vuefire를 설치합니다.

```
import VueFire from "vuefire";
import firebase from "firebase";

Vue.use(firebase);
Vue.use(VueFire);
```

main.js에 vuefire와 firebase를 import하여 Vue.use를 통해 등록합니다.

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

을 통해 firebase와 연결합니다.

```
const comentsRef = firebase.database().ref(`Coments`);
```

를 통해 firebase에 미리 만든 comentsRef를 통해 Coments테이블에 접근합니다.

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

vuefire로 omentsRef를 통해 접근한 Coments의 데이터들을 Coments로 바인딩 해줍니다.

```
comentsRef.push(this.newComent);
```

comentsRef.push를 통해 AddComent.vue에서 전달받은 새로운 데이터를 firebase의 Coments테이블에 저장합니다.

각각의 데이터에는 키가 .key의 형태로 자동으로 할당이 되며

````
comentsRef.child(user[".key"]).remove();
```

키를 통해 데이터에 접근하여 remove를 통해 데이터를 삭제할 수 있습니다.

## 느낀점

firebase의 사용법이 잘되 있어서 적용하기도 쉽고 이용하는 것 자체도 어렵지 않았다.

firebase의 실시간 데이터 베이스를 이용하여, 실시간으로 데이터를 저장하고 삭제하는 것을 통해
간단한 프로젝트를 위한 백엔드로 사용하도 괜찮다고 생각했다.

firebase는 주로 인증서비스 구현을 위해 많이 사용한다고 들었는데 그런 인증서비스도 한번 구현해 보고 싶다.
```
````
