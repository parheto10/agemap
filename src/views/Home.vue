<template>
  <div class="home">
<!--    <img alt="Vue logo" src="../assets/logo.png">-->
<!--    <HelloWorld msg="Welcome to Your Vue.js App"/>-->
    <Map />
  </div>
</template>

<script>
import Map from "@/components/Map";
export default {
  name: 'Home',
  components: {
    Map
  }
}
</script>
