<template>
  <div id="app">
    <header>
      <div id="title">Stress test results</div>
    </header>
    <router-view />
  </div>
</template>

<style lang="scss">
@import url("https://fonts.googleapis.com/css2?family=Roboto&display=swap");

body {
  margin: 0;
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
  height: 15vh;
  background-color: rgb(239, 50, 129, 0.5);
  box-shadow: 0 2px 3px -3px black;
  #title {
    font-size: x-large;
    font-weight: bold;
  }
}
</style>
