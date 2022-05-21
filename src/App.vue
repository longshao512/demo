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
}

body {
  margin: 0px;
  padding: 0px;
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
