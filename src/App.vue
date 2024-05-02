<script setup>
import Player from './components/Player.vue';

//importando backgrounds
import background1 from '../src/assets/images/pixel_art/background1.gif';
import background2 from '../src/assets/images/pixel_art/background2.gif';
import background3 from '../src/assets/images/pixel_art/background3.gif';
import background4 from '../src/assets/images/pixel_art/background4.gif';
import background5 from '../src/assets/images/pixel_art/background5.gif';
import background6 from '../src/assets/images/pixel_art/background6.jpg';
import background7 from '../src/assets/images/pixel_art/background7.gif';
import background8 from '../src/assets/images/pixel_art/background8.gif';
import background9 from '../src/assets/images/pixel_art/background9.gif';
import background10 from '../src/assets/images/pixel_art/background10.gif';
import background11 from '../src/assets/images/pixel_art/background11.gif';
import background12 from '../src/assets/images/pixel_art/background12.gif';
import background13 from '../src/assets/images/pixel_art/background13.gif';

import song1 from '../src/assets/music/The Last Goodbye.mp3';
import song2 from '../src/assets/music/We loved.mp3';
import song3 from '../src/assets/music/Have You Ever Seen The Rain.mp3';
import song4 from '../src/assets/music/Puedes Contar Conmigo.mp3';

const backgrounds = [background1, background2, background3, background4,  background5, background6, 
                      background7, background8, background9, background10, background11, background12, background13];
const currentBackground = backgrounds[Math.floor(Math.random() * backgrounds.length)];

const songs = [
  { title: 'The Last Goodbye', artist: 'Billy boyd', file: song1 },
  { title: 'We Loved', artist: '스무살, 볼빨간사춘기', file: song2 },
  { title: 'Have Your Ever Seen The Rain', artist: 'Creedence Clearwater Revival', file: song3},
  { title: 'Puedes Contar Conmigo', artist: 'La Oreja de Van Gogh', file: song4}
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
