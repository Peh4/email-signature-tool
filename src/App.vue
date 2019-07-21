<template>
  <div id="app">
    <router-view/>
  </div>
</template>

<style lang="scss">
@import 'assets/style.scss';

#app {
  width: 100%;
  background: #02a0a5 none;
  & > * {
    background: #fff none;
    padding: 0;
    max-width: 800px;
    margin: 0 auto;
  }
}
</style>