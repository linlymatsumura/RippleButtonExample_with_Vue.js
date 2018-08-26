<template>
  <div id="app">
      <my-button @click="onClick">BUTTON</my-button>
      <my-button @click="onClick" disabled>DISABLED</my-button>
      <div>{{ clickCount }} clicked</div>
  </div>
</template>

<script>
import MyButton from "./components/MyButton";

export default {
  name: "App",
  components: {
    MyButton
  },
  data () {
    return {
      clickCount: 0
    }
  },
  methods: {
    onClick () {
      this.clickCount++;
    }
  }
};
</script>

<style lang="scss" scoped>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
