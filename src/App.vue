<template>
  <div id="app">
    <header class="shadow-sm">
      <div id="title">Stress test results</div>
    </header>
    <router-view />
  </div>
</template>

<style lang="scss">
@import url("https://fonts.googleapis.com/css2?family=Roboto&display=swap");
@import "~bootstrap/scss/bootstrap";
body {
  margin: 0;
  background-color: $gray-200;
}
#app {
  font-family: Roboto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

header {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 10vh;
  background-color: $teal;
  box-shadow: 0 2px 3px -3px black;
  #title {
    font-size: x-large;
    color: $gray-600;
  }
}
</style>
