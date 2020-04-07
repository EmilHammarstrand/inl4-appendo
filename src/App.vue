<template>
  <div id="app">
    <Form />
    <Home />
    <List />
  </div>
</template>

<script>

import Form from "./components/Form"
import Home from "./components/Home"
import List from "./components/List"
export default {
  name: 'App',
  components: {
    Form,
    Home,
    List
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>
