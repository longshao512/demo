<template>
  <div id="app">
    <div id="nav">
      <router-link to="/"></router-link>   
    </div>
    <router-view/>
  </div>
</template>

<style lang="less">
.app {
  height: 100%;
  width: 100vw;
}

body {
  margin: 0px;
  padding: 0px;
  width: 100vw;
}

html, body {
  height: 100%;
  background-color: #fff;
  color: #333;
}

* {
  padding: 0;
  margin: 0;
}

</style>
