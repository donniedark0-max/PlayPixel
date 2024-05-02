<template>
  <div class="player">
    <button class="play-button" @click="togglePlay">{{ isPlaying ? 'Pause' : 'Play' }}</button>
    <p v-if="currentSong">{{ currentSong.title }} - {{ currentSong.artist }}</p>
    <div class="progress-bar">
      <div class="progress" :style="{ width: progressWidth }"></div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, computed } from 'vue';

const props = defineProps({
  initialSong: Object
});

const currentSong = ref(null);
let audio = null;
const isPlaying = ref(false);
const progress = ref(0);


onMounted(() => {
  currentSong.value = props.initialSong;
});

// Función para alternar entre reproducir y pausar la canción
function togglePlay() {
  if (!audio) {
    audio = new Audio(currentSong.value.file);
    audio.play();
    isPlaying.value = true;
    audio.addEventListener("timeupdate", updateProgress);
    audio.addEventListener('ended', () => {
      isPlaying.value = false;
    });
  } else {
    if (audio.paused) {
      audio.play();
      isPlaying.value = true;
    } else {
      audio.pause();
      isPlaying.value = false;
    }
  }
}

// Función para actualizar el progreso de la canción
function updateProgress() {
  progress.value = (audio.currentTime / audio.duration) * 100 + '%';
}

// Calcula el ancho de la barra de progreso
const progressWidth = computed(() => {
  return progress.value;
});

</script>

<style scoped>
.player {
  background-color: rgba(0, 0, 0, 0.7); /* Adjust opacity for readability */
  color: white;
  padding: 1rem;
  border-radius: 5px;
}
.play-button {
  margin-left: 4.5rem;
  background-color: #007bff;
  color: white;
  border: none;
  padding: 0.5rem 1rem;
  border-radius: 5px;
  cursor: pointer;
}

.progress-bar {
  width: 100%;
  height: 10px;
  background-color: #ccc;
  margin-top: 1rem;
}

.progress {
  height: 100%;
  background-color: #ea0e0e;
}
</style>
