<template>
  <div class="player">
    <p v-if="currentSong">
      <span>{{ currentSong.title }} - {{ currentSong.artist }}</span>
    </p>
    <div class="controls">
      <div class="progress-bar" @click="seek">
        <div class="progress" :style="{ width: progressWidth }"></div>
      </div>
    </div>

      <div class="time-info">
        <span>{{ formatTime(currentTime) }} - {{ formatTime(duration) }}</span>
      </div>
    
    <div class="volume-control" @mouseenter="showVolume = true" @mouseleave="showVolume = false">
      <span>🔊</span>
      <div v-show="showVolume" class="volume-bar" @click="changeVolume">
        <div class="volume-progress" :style="{ width: volumeWidth }"></div>
      </div>
    </div>
    <button class="play-button" @click="togglePlay">{{ isPlaying ? 'Pause' : 'Play' }}</button>
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
const currentTime = ref(0);
const duration = ref(0);
const showVolume = ref(false);

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
    audio.addEventListener("timeupdate", updateTime);
    audio.addEventListener("loadedmetadata", () => {
      duration.value = audio.duration;
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

//funcion para actualizar el tienmpo de reprod
function updateTime() {
  if (audio){
    currentTime.value = audio.currentTime;
  }
}

//funcion para adeknatar o retroceder en la cancion
function seek(event) {
  const progressBar = event.currentTarget;
  const clickPosition = event.clientX - progressBar.getBoundingClientRect().left;
  const progressPercentage = (clickPosition / progressBar.offsetWidth) * 100;
  const seektTime = (audio.duration * progressPercentage) / 100;
  audio.currentTime = seektTime;
  
}

//function para formatear el tiempo en formato mm:ss
function formatTime(time) {
  const minutes = Math.floor(time / 60);
  const seconds = Math.floor(time % 60);
  return `${minutes}:${seconds.toString().padStart(2,'0')}`;
}


//funcion para cambiar el volumen
function changeVolume(event) {
  const volumeBar = event.currentTarget;
  const clickPosition = event.clientX - volumeBar.getBoundingClientRect().left;
  const volumePercentage = (clickPosition / volumeBar.offsetWidth) * 100;
  audio.volume = volumePercentage / 100;
}
// Calcula el ancho de la barra de progreso
const progressWidth = computed(() => {
  return progress.value;
});

// Calcula el ancho de la barra de volumen
const volumeWidth = computed(() => {
  if (audio) {
    return (audio.volume * 100) + '%';
  } else{
    return '0%';
  }
});
</script>

<style scoped>
.player {
  background-color: rgba(0, 0, 0, 0.7); /* Adjust opacity for readability */
  color: white;
  padding: 1rem;
  border-radius: 5px;
  text-align: center;
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

.controls{
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-top: 1rem;
}
.progress-bar {
  flex: 1;
  height: 10px;
  background-color: #ccc;
  cursor: pointer;
}

.progress {
  height: 100%;
  background-color: #ea0e0e;
}


.volume-bar {
  width: 100%;
  height: 10px;
  background-color: rgba(255, 255, 255, 0.5);
  position: initial;
  cursor: pointer;
}

.volume-progress {
  height: 100%;
  background-color: #007bff;
}

.volume-control {
  display: flex;
  align-items: center;
  justify-content:start;
  margin-top: 1rem;
  position: relative;
}

</style>
