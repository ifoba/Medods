<template>
  <div id="app">
    <div class="box">
      <div class="game-container">
        <Button v-for="col in color" :key="col" :color="col"/>
        <div class="center">Simon The Game</div>
      </div>
    </div>
  </div>
</template>

<script>
import Button from "./components/Button.vue";
export default {
  name: "App",
  components: {
    Button,
  },
  data: () => {
    return {
      color: {
        first: "red",
        second: "green",
        third: "yellow",
        fourth: "cadetblue",
      },
    };
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
.box {
  position: relative;
  width: 400px;
  height: 400px;
}
.game-container {
  display: flex;
  width: 400px;
  flex-wrap: wrap;
  border-radius: 30%;
  border: 2px solid black;
  overflow: hidden;
}
.center {
  width: 200px;
  height: 100px;
  color: black;
  background: white;
  border-radius: 40px;
  position: absolute;
  top: 150px;
  left: 100px;
  display: flex;
  align-items: center;
  justify-content: center;
}
</style>
