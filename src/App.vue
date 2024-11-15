<template>
  <CarrouselPersonnages/>
</template>

<script>
import CarrouselPersonnages from './components/CarrouselPersonnages.vue'

export default {
  name: 'App',
  components: {
    CarrouselPersonnages
  }
}
</script >

<style  lang="scss" >
@import "css/global.scss";

body {
  background-color: #000000;
}
</style>
