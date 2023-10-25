<template>
    <div>
      <select class="lang" v-model="languagehome" style = "width:16.5vw" >
                <option value="" disabled >selected Languages</option>
                        <option value="English">English</option>
                        <option value="Malayalam">Malayalam</option>
                        <option value="Tamil">Tamil</option>
                        <option value="Teluhu">Teluhu</option>
                        <option value="Kannada">Kannada</option>
                        <option value="Hindi">Hindi</option>
                    </select>
      <button @click="togglePlay"><img v-if="!isPlaying" src="./playbtn.png" alt="Play" style="width: 20px; height: 20px;">
      <img v-else src="./pause-button.png" alt="Pause" style="width: 20px; height: 20px;"></button>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        languagehome:'',
        isPlaying: false,
        audio: null,
        audioSources: {
        English: '/english.mp4', // Replace with the path to your English audio file
        Malayalam: '/malayalam.mp4', // Replace with the path to your Malayalam audio file
        Tamil: '/tamil.mp4', // Replace with the path to your Tamil audio file
        Teluhu: '/telugu.mp4', // Replace with the path to your Teluhu audio file
        Kannada: '/kannada.mp4', // Replace with the path to your Kannada audio file
        Hindi: '/hindi.mp4', // Replace with the path to your Hindi audio file
      }
      };
    },
    methods: {
       togglePlay() {
      if (!this.audio) {
        this.audio = new Audio(this.audioSources[this.languagehome]);
      }

      if (this.isPlaying) {
        this.audio.pause();
        this.isPlaying = false;
      } else {
        this.audio.play();
        this.isPlaying = true;
      }
    }
      // togglePlay() {
      //   if (!this.audio) {
      //   this.audio = new Audio('/neelanilave.mp3'); // Update the file path if necessary
      // }

      // if (this.isPlaying) {
      //   this.audio.pause();
      //   this.isPlaying = false;
      // } else {
      //   this.audio.play();
      //   this.isPlaying = true;
      // }
      // },
    },
  };
  </script>
  
  <style>
  /* Add your styles here */
  </style>