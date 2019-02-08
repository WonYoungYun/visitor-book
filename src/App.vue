<template>
  <div id="app">
    <visitor-book class="container"></visitor-book>
  </div>
</template>

<script>
import VisitorBook from "./components/VisitorBook.vue";
export default {
  name: "app",
  components: {
    VisitorBook
  }
};
</script>

<style>
html,
body {
  padding: 0;
  margin: 0;
}
h1 {
  margin: 0;
}
textarea {
  resize: none;
}
::-webkit-scrollbar {
  display: none;
}
</style>
