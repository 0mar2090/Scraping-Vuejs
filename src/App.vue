<template>
  <div id="app">
    <div class="container">
      <div class="box-container">
        <div class="box" @click="ClickApi('moda')">
          <div class="image">
            <img src="https://mmo.aiircdn.com/766/6501d6f26b580.png" alt="" />
          </div>
          <div class="content">
            <h3>Radio Moda</h3>
          </div>
        </div>
        <div class="box" @click="ClickApi('lainolvidable')">
          <div class="image">
            <img src="https://mmo.aiircdn.com/766/6501d6f1c8dd9.png" alt="" />
          </div>
          <div class="content">
            <h3>Radio La Inolvidable</h3>
          </div>
        </div>

        <div class="box" @click="ClickApi('radiomar')">
          <div class="image">
            <img src="https://mmo.aiircdn.com/766/6501d6f315712.png" alt="" />
          </div>
          <div class="content">
            <h3>Radiomar</h3>
          </div>
        </div>
        <div class="box" @click="ClickApi('magica')">
          <div class="image">
            <img src="https://mmo.aiircdn.com/766/6501d6f1f0119.png" alt="" />
          </div>
          <div class="content">
            <h3>Radio Magica</h3>
          </div>
        </div>
        <div class="box" @click="ClickApi('ritmoromantica')">
          <div class="image">
            <img src="https://mmo.aiircdn.com/766/6501d6f39ffb1.png" alt="" />
          </div>
          <div class="content">
            <h3>Radio Ritmo Romantica</h3>
          </div>
        </div>
        <div class="box" @click="ClickApi('nuevaq')">
          <div class="image">
            <img src="https://mmo.aiircdn.com/766/6501d6f2ed22c.png" alt="" />
          </div>
          <div class="content">
            <h3>Radio Nueva Q</h3>
          </div>
        </div>
        <div class="box" @click="ClickApi('planeta')">
          <div class="image">
            <img src="https://mmo.aiircdn.com/766/6501d6f376e86.png" alt="" />
          </div>
          <div class="content">
            <h3>Radio Planeta</h3>
          </div>
        </div>
        <div class="box" @click="ClickApi('bienestar')">
          <div class="image">
            <img src="https://mmo.aiircdn.com/766/6501d6f11ac4b.png" alt="" />
          </div>
          <div class="content">
            <h3>Radio Bienestar</h3>
          </div>
        </div>
        <div class="box" @click="ClickApi('incasat')">
          <div class="image">
            <img src="https://mmo.aiircdn.com/766/6501d6f118db6.png" alt="" />
          </div>
          <div class="content">
            <h3>Radio Inca Sat</h3>
          </div>
        </div>
      </div>
    </div>

    <div class="music-player active">
      <div id="close-player" class="fas fa-angle-up fa-times"></div>
      <h3 class="music-title">{{ radioName }}</h3>
      <audio-player :stream-url="streamUrl"></audio-player>
    </div>
  </div>
</template>

<script>
import AudioPlayer from "./components/AudioPlayer.vue";
import axios from "axios";

export default {
  components: {
    "audio-player": AudioPlayer,
  },
  data() {
    return {
      streamUrl: null,
      radioName: "",
      imageUrl: "",
      search: "lainolvidable",
      api: "http://localhost:3000",
    };
  },
  mounted() {
    this.fetchStreamInfo();
  },
  methods: {
    async fetchStreamInfo() {
      try {
        const response = await axios.get(
          `${this.api}/api/live?search_query=${this.search}`
        );
        const data = response.data;
        const { streamUrl, radioName, imageUrl } = data;
        this.streamUrl = streamUrl;
        this.radioName = radioName;
        this.imageUrl = imageUrl;
      } catch (error) {
        console.error(
          "Error al obtener la información de la radio:",
          error.message
        );
      }
    },
    ClickApi(newEmi) {
      // Actualizar el valor de emi cuando se hace clic en una imagen
      this.search = newEmi;
      this.fetchStreamInfo(); // Volver a cargar la información con la nueva emi
    },
  },
};
require('./assets/css/style.css');

</script>

