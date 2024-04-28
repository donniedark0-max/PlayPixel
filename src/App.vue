<script setup>
import Player from './components/Player.vue';
import background1 from '../src/assets/images/pixel_art/background1.gif'; // Replace with your pixel art image
import background2 from '../src/assets/images/pixel_art/background2.gif'; // Optional, another calming background

// Optional: Add logic for switching backgrounds
let currentBackground = background1;
// ... (code to handle background change, e.g., button click)

</script>

<template>
  <div class="app" :style="{ backgroundImage: `url(${currentBackground})` }">
    <Player />
  </div>
</template>

<style scoped>
.app {
  position: absolute;
  top: s0;
  left: 0;
  width: 100vw;
  height: 100vh;
  background-size: cover;
  background-position: center;
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
