<template>
  <div class="container">
    <div class="row">
      <div class="col-6">
        <div class="position-fixed"><div id="map"></div></div>
      </div>
      <div class="col-6 text-left">
        <button
          type="button"
          v-html="getButtonTitle"
          class="create-button text-center"
          @click="isFormHidden = !isFormHidden"
        ></button>
        <MemoryCreate v-if="!isFormHidden" />
        <br />
        <hr />
        <br />
        <h4><strong>Valentine's Day at Maggianos pasta 🍝</strong></h4>
        <h6><strong>Feb 14th, 2020</strong></h6>
        <p>
          We went on a lovely date to Maggianos Little Italy and got some
          delicious pasta. The waitress sat us next to the kitchen which was a
          bit annoying but you got to sit in a spot where you could see a little
          baby playing!
        </p>
        <hr />
        <br />
      </div>
    </div>
  </div>
</template>

<script>
var mapboxgl = require("mapbox-gl");
var MapboxGeocoder = require("mapbox-gl-geocoder");
import "mapbox-gl-geocoder/dist/mapbox-gl-geocoder.css";

import MemoryCreate from "../components/MemoryCreate";

export default {
  name: "Home",
  components: {
    MemoryCreate,
  },
  data() {
    return {
      isFormHidden: true,
      apiKey:
        "pk.eyJ1Ijoicml0d2lrZGl2IiwiYSI6ImNrbXQ3dzB5OTBwNjAycG54b2FqM2J5N2gifQ.bVO6sXRv29Y6d57cicHUOg",
    };
  },
  mounted() {
    this.createMap();
  },
  computed: {
    getButtonTitle() {
      if (this.isFormHidden == false) {
        return `<svg xmlns="http://www.w3.org/2000/svg" width="25" height="25" fill="#2c3e50" class="bi bi-dash-square-fill" viewBox="0 0 16 16">
  <path d="M2 0a2 2 0 0 0-2 2v12a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V2a2 2 0 0 0-2-2H2zm2.5 7.5h7a.5.5 0 0 1 0 1h-7a.5.5 0 0 1 0-1z"/>
</svg>`;
      } else {
        return `<svg xmlns="http://www.w3.org/2000/svg" width="25" height="25" fill="#2c3e50" class="bi bi-plus-square-fill" viewBox="0 0 16 16">
  <path d="M2 0a2 2 0 0 0-2 2v12a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V2a2 2 0 0 0-2-2H2zm6.5 4.5v3h3a.5.5 0 0 1 0 1h-3v3a.5.5 0 0 1-1 0v-3h-3a.5.5 0 0 1 0-1h3v-3a.5.5 0 0 1 1 0z"/>
</svg>`;
      }
    },
  },
  methods: {
    createMap() {
      mapboxgl.accessToken = this.apiKey;
      this.map = new mapboxgl.Map({
        container: "map",
        style: "mapbox://styles/ritwikdiv/ckmttqrnh4chg17s44d08w26q",
        minzoom: 1.3,
        center: [-87.629, 41.878], // Manhattan
        zoom: 12,
      });
      this.map.addControl(
        new MapboxGeocoder({
          accessToken: mapboxgl.accessToken,
          mapboxgl: mapboxgl,
        })
      );
    },
  },
};
</script>

<style scoped>
#map {
  height: 600px;
  width: 500px;
  border-radius: 5px;
}
.create-button {
  background-color: white;
  border: none;
  text-decoration: none;
  text-align: center;
  display: inline-block;
}

.create-button:focus {
  outline: none;
}
</style>
