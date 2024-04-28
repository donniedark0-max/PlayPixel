<template>
    <div class="player">
      <button @click="$emit('play')">Play</button>
      <button @click="$emit('pause')">Pause</button>
      <p>Now Playing: {{ currentSong.title }} - {{ currentSong.artist }}</p>
    </div>
  </template>
  
  <script setup>
  import { ref } from 'vue';
  
  const currentSong = ref({ title: '', artist: '' });
  
  // Function to update song info based on your music library logic
  function updateSong(newSong) {
    currentSong.value = newSong;
  }
  
  // Emit events for play/pause functionality
  function playSong() {
    $emit('play');
  }
  
  function pauseSong() {
    $emit('pause');
  }
  
  </script>
  
  <style scoped>
  .player {
    background-color: rgba(0, 0, 0, 0.7); /* Adjust opacity for readability */
    color: white;
    padding: 1rem;
    border-radius: 5px;
  }
  </style>
  