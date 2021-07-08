<template>
  <div id='app'>
    <sample-three-view />
  </div>
</template>

<script lang='ts'>
import {defineComponent} from 'vue'
import SampleThreeView from "./view/SampleThreeView.vue";

export default defineComponent({
  name: 'App',
  components: {SampleThreeView}
})
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  width: 100vw;
  height: 100vh;
}
</style>
