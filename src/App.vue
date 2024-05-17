<script setup>
import { RouterLink, RouterView } from 'vue-router'
import Navbar from '@/components/Navbar.vue'
</script>

<template>
  <div class="main">
    <Navbar class="na"/>
    <RouterView class="ad" />
    <Footer>
      <p><i>powered by xorzz</i></p>
    </Footer>
  </div>

</template>

<style lang="scss">
$primary-color: #111c29;


.main {
  background-color: $primary-color;
  color: whitesmoke;


  .ad {
    position: relative;
    z-index: 1;
  }
  .na{
    position: absolute;
    z-index: 2;

  }

  Footer {
    display: flex;
    background-color: #0e1723;
    justify-content: center;
    align-items: center;
    height: 2rem;

    p {
      color: rgb(64, 64, 64);
      font-size: small;
      margin: 0;
      transition: all 0.5s ease; 
    }

    p:hover {
      text-decoration: none !important;
      color: aqua;
      cursor:pointer;
    }
  }
}
</style>
