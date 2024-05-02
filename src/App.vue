<script setup>
import Player from './components/Player.vue';

import background1 from '../src/assets/images/pixel_art/background1.gif';
import background2 from '../src/assets/images/pixel_art/background2.gif';

import song1 from '../src/assets/music/The Last Goodbye.mp3';
import song2 from '../src/assets/music/We loved.mp3';

const backgrounds = [background1, background2];
const currentBackground = backgrounds[Math.floor(Math.random() * backgrounds.length)];

const songs = [
  { title: 'The Last Goodbye', artist: 'Billy boyd', file: song1 },
  { title: 'We Loved', artist: '스무살, 볼빨간사춘기', file: song2 }
];

const selectedSong = songs[Math.floor(Math.random() * songs.length)];

</script>

<template>
  <div class="app" :style="{ backgroundImage: `url(${currentBackground})` }">
    <Player :initialSong="selectedSong"/>
  </div>
</template>

<style scoped>
.app {
  position: absolute;
  top: 0;
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
