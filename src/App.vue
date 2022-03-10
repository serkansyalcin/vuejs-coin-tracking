<template>
  <div class="cantainer">
    <TheTrackir />
    
  </div>
</template>

<script>
import TheTrackir from './components/The-Trackir.vue'

export default {
  name: 'App',
  components: {
    TheTrackir,
  }
}
</script>

<style>
  * {
      padding: 0;
      margin: 0;
      box-sizing: border-box;
      outline: none;
      list-style: none;
      font-size: 100%;
  }

  * button:hover {
    opacity: 0.5;
    transition: 300ms opacity;
  }

  .cantainer {
    position: relative;
    width: 100%;
    height: 100vh;
    background-color: #E5E5E5;
  }


</style>
