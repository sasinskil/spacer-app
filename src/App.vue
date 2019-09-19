<template>
  <div class="app">
    <div class="nav">
      <router-link to="/">spacer</router-link> | 
      <router-link to="/about">about</router-link>
    </div>
    <router-view/>
  </div>
</template>

<style lang="scss" scoped>

@import url('https://fonts.googleapis.com/css?family=Montserrat:400,700&display=swap&subset=latin-ext');

.app {
  font-family: 'Montserrat', sans-serif;
}

</style>
