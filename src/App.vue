<template>
  <GuideComponent/>
</template>

<script>
import GuideComponent from './components/Guide.vue'

export default {
  name: 'App',
  components: {
    GuideComponent
  }
}
</script>

<style>
#app {
  font-family: 'Open Sans', sans-serif;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 97vh;
}
</style>
