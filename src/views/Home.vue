<template>
  <div class="container">
    <div class="row d-lg-flex">
      <div class="col-lg-4">
        <div class="position-fixed"><div id="map"></div></div>
      </div>
      <div class="col-lg-8 overflow-auto">
        <h1>asdfkjahdfasdf</h1>
        <h1>asdfkjahdfasdf</h1>
        <h1>asdfkjahdfasdf</h1>
        <h1>asdfkjahdfasdf</h1>
        <h1>asdfkjahdfasdf</h1>
        <h1>asdfkjahdfasdf</h1>
        <h1>asdfkjahdfasdf</h1>
        <h1>asdfkjahdfasdf</h1>
        <h1>asdfkjahdfasdf</h1>
        <h1>asdfkjahdfasdf</h1>
        <h1>asdfkjahdfasdf</h1>
        <h1>asdfkjahdfasdf</h1>
        <h1>asdfkjahdfasdf</h1>
        <h1>asdfkjahdfasdf</h1>
        <h1>asdfkjahdfasdf</h1>
        <h1>asdfkjahdfasdf</h1>
        <h1>asdfkjahdfasdf</h1>
        <h1>asdfkjahdfasdf</h1>
      </div>
    </div>
  </div>
</template>

<script>
var mapboxgl = require("mapbox-gl");
var MapboxGeocoder = require("mapbox-gl-geocoder");
import "mapbox-gl-geocoder/dist/mapbox-gl-geocoder.css";

export default {
  name: "Home",
  data() {
    return {
      apiKey:
        "pk.eyJ1Ijoicml0d2lrZGl2IiwiYSI6ImNrbXQ3dzB5OTBwNjAycG54b2FqM2J5N2gifQ.bVO6sXRv29Y6d57cicHUOg",
    };
  },
  mounted() {
    this.createMap();
  },
  methods: {
    createMap() {
      mapboxgl.accessToken = this.apiKey;
      this.map = new mapboxgl.Map({
        container: "map",
        style: "mapbox://styles/ritwikdiv/ckmt7wusz1xmy17o6lfwkr786",
        minzoom: 1.3,
        center: [-74.0073, 40.7124], // Manhattan
        zoom: 16,
      });
      // this.map.addControl(new mapboxgl.Navigation());
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
</style>
