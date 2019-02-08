<template>
  <div class="add-coment">
    <form @submit.prevent="$emit('commit', user)" class="add-coment-form">
      <div>
        <input
          type="text"
          id="name-input"
          v-model="user.name"
          maxlength="11"
          required
          autocomplete="off"
        >
        <label for="name-input">이름</label>
      </div>
      <div>
        <textarea
          id="coment-input"
          ref="inputText"
          v-model="user.coment"
          @keyup="checkByte"
          required
        ></textarea>
        <label for="coment-input">남기고 싶은 말</label>
        <span class="textarea-counter">{{wordCount}}/{{maxComent}}</span>
      </div>
      <div class="btn-area">
        <button
          class="btn-success"
          :class="{abled:!isValidInput}"
          type="submit"
          :disabled="isValidInput"
        >등록</button>
        <a href class="cancle-coment-button" @click.prevent="$emit('close')">&times;</a>
      </div>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      user: {
        name: "",
        coment: ""
      },
      wordCount: 0,
      coment: "",
      maxComent: 100
    };
  },
  computed: {
    isValidInput() {
      return !this.user.name || !this.user.coment;
    }
  },
  methods: {
    checkByte(e) {
      if (e.target.value.length <= this.maxComent) {
        this.coment = e.target.value;
        this.wordCount = e.target.value.length;
      } else e.target.value = this.coment;
    }
  }
};
</script>

<style scoped>
input,
textarea {
  width: 100%;
  box-sizing: border-box;
  box-shadow: none;
  outline: none;
  border: none;

  border-bottom: 2px solid #999;
}

.add-coment {
  width: 400px;
  background: #fff;
  padding: 40px;
  border: 1px solid rgba(0, 0, 0, 0.1);
  box-shadow: 0 5px 10px rgba(0, 0, 0, 0.2);
}
.add-coment-form {
  position: relative;
}
.add-coment-form div {
  position: relative;
}
.add-coment-form label {
  position: absolute;
  top: 0;
  left: 0;
  color: #999;
  font-size: 18px;
  transition: 0.5s;
  pointer-events: none;
}

#name-input {
  padding: 10px 0 5px 0;
  margin-bottom: 30px;
  font-size: 16px;
  font-weight: 700;
}
#coment-input {
  height: 80px;
  padding: 15px 10px 5px 0;
  font-size: 16px;
  font-style: "sans-serif";
  font-weight: 700;
  margin-bottom: 20px;
}

#name-input:valid ~ label,
#coment-input:valid ~ label,
#name-input:focus ~ label,
#coment-input:focus ~ label {
  top: -30px;
  left: 0;
  color: #41b883;
  font-size: 16px;
  font-weight: 700;
}

#name-input:valid,
#coment-input:valid,
#name-input:focus,
#coment-input:focus {
  border-bottom: 2px solid #41b883;
}
.textarea-counter {
  position: absolute;
  right: 0;
  top: 30px;
  transform: translate(0, -100%);
}
.btn-area {
  position: relative;
  height: 50px;
  display: flex;
  justify-content: center;
  align-items: center;
}
.cancle-coment-button {
  text-decoration: none;
  width: 30px;
  height: 40px;
  text-align: center;
  background-color: #ccc;
  color: #999;
  font-size: 30px;
  font-weight: 700;
  border-radius: 0 10px 10px 0;
  line-height: 1;
  transition: 0.5s;
}
.cancle-coment-button:hover {
  background-color: red;
  color: #fff;
}
.btn-success {
  border: none;
  outline: none;
  width: 100px;
  height: 40px;
  font-size: 18px;
  font-weight: 700;
  border-radius: 10px 0 0 10px;
}
.abled {
  color: #fff;
  background-color: #41b883;
  cursor: pointer;
}
</style>
