<template>
  <div id="visitor-book">
    <h1 class="title">방명록</h1>
    <div class="coments-area">
      <div v-for="(item,index) in Coments" :key="index" class="user-area">
        <div class="user-header">
          <span class="user-id">{{item.name}} :&nbsp;</span>
          <span class="write-date">{{item.date}}</span>
        </div>
        <span class="user-coment">{{item.coment}}</span>
        <a href class="coment-delete" @click.prevent="deleteComent(item)">&times;</a>
      </div>
    </div>
    <div class="button-area">
      <div v-if="isAddComent" class="add-coment">
        <add-coment @close="isAddComent=false" @commit="writeComent"></add-coment>
      </div>
      <div v-else>
        <a href class="add-coment-btn" @click.prevent="isAddComent=true">글쓰기</a>
      </div>
    </div>
  </div>
</template>

<script>
import AddComent from "./AddComent.vue";
import firebase from "firebase";
import { config } from "../config/index.js";

firebase.initializeApp(config);

const comentsRef = firebase.database().ref(`Coments`);

export default {
  components: {
    AddComent
  },
  computed: {},
  firebase: {
    Coments: comentsRef
  },

  data() {
    return {
      isAddComent: false,
      newComent: {
        name: "",
        coment: "",
        date: ""
      }
    };
  },
  created() {},
  methods: {
    writeComent(user) {
      this.isAddComent = false;
      this.newComent.name = user.name;
      this.newComent.coment = user.coment;
      this.newComent.date = user.date;
      comentsRef.push(this.newComent);
      this.newComent = {};
    },
    deleteComent(user) {
      if (confirm("방명록을 삭제하시겠습니까?"))
        return comentsRef.child(user[".key"]).remove();
      else return;
    }
  }
};
</script>

<style scoped>
#visitor-book {
  display: flex;
  flex-direction: column;
  margin: 80px auto;
  width: 800px;
  height: 1000px;
  border: 3px solid #41b883;

  box-shadow: 0 5px 10px rgba(0, 0, 0, 0.2);
  box-sizing: border-box;
}
.title {
  flex: 1;
  margin: 30px 0 20px 0;
  text-align: center;
  box-sizing: border-box;
}
.coments-area {
  flex: 10;
  padding: 20px;
  width: 100%;

  box-sizing: border-box;
  border-top: 2px solid #41b883;
  overflow-y: scroll;
}
.user-area {
  position: relative;
  margin-bottom: 5px;
  width: 100%;
  border: 1px solid #41b883;
  box-shadow: 0 5px 10px rgba(0, 0, 0, 0.2);
}

.user-id {
  display: inline-block;
  margin: 10px 0 10px 10px;
}
.write-date {
  position: absolute;
  top: 0;
  right: 0;
  transform: translate(-50%, 50%);
}
.user-coment {
  display: block;
  font-style: "sans-serif";
  margin: 5px 35px 10px 35px;
  padding: 10px;
  background-color: #fee;
  font-weight: 700;
  box-sizing: border-box;
}
.coment-delete {
  position: absolute;
  right: 0;
  top: 50%;
  font-size: 24px;
  text-decoration: none;
  color: #333;
  transform: translate(-20%, -60%);
}
.button-area {
  flex: 1;
  position: relative;
  height: 60px;
  border-top: 2px dashed #41b883;
  text-align: center;
  line-height: 60px;
}
.add-coment {
  position: absolute;
  top: -200%;
  left: 50%;
  transform: translate(-50%, -50%);
}
.add-coment-btn {
  margin-top: 10px;
  display: inline-block;
  width: 120px;
  height: 40px;
  line-height: 40px;
  text-decoration: none;
  color: #fff;
  font-weight: 700;
  border-radius: 15px;
  background-color: #41b883;
}
@media screen and (max-width: 800px) {
  #visitor-book {
    width: 100%;
    height: 100vh;
    margin: 0;
  }
  .add-coment {
    top: 50;
    left: 50%;
  }
}
</style>
