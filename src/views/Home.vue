<template>
  <div class="container">
    <div class="row">
      <div class="col-6">
        <div class="position-fixed"><div id="map"></div></div>
      </div>
      <div class="col-6 text-left overflow-auto">
        <button
          type="button"
          v-html="getButtonTitle"
          class="create-button text-center"
          @click="isFormHidden = !isFormHidden"
        ></button>
        <MemoryCreate v-if="!isFormHidden" />
        <br />
        <br />
        <div
          class="post p-1"
          v-for="post in posts"
          :key="post.id"
          v-bind:id="post.id"
        >
          <h5>
            <strong>{{ post.title }}</strong>
          </h5>
          <h6 class="mt-3">
            <strong
              ><span class="text-info">{{ convertDate(post.date) }}</span> ●
              <span class="text-warning">
                {{ post.location_desc }}
              </span></strong
            >
          </h6>
          <p class="desc mt-3">{{ post.desc }}</p>
          <hr />
        </div>
        <br />
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
      map: null,
      posts: [
        {
          id: "1",
          title: "Valentine's Day 2020 🍝",
          date: "02/14/2020",
          location_desc: "Maggiano's Little Italy",
          coordinates: [-87.631437, 41.891412],
          desc:
            "We went on a lovely date to Maggianos Little Italy and got some delicious pasta. The waitress sat us next to the kitchen which was a bit annoying but you got to sit in a spot where you could see a little baby playing!",
        },
        {
          id: "2",
          title: "Anniversary - Hamilton 🎶",
          date: "05/22/2018",
          location_desc: "CIBC Theater",
          coordinates: [-87.627411, 41.885400000000004],
          desc:
            "We went to watch Hamilton for our first anniversary! It was absolutely wonderful and everything we hoped for. Topping that might be hard!",
        },
      ],
    };
  },
  mounted() {
    this.createMap();
    this.addMarkers();
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
    addMarkers() {
      for (var post of this.posts) {
        var el = document.createElement("a");
        el.href = `#${post.id}`;
        el.innerHTML = `<svg xmlns="http://www.w3.org/2000/svg" width="32" height="32" fill="#355070" class="bi bi-geo-fill" viewBox="0 0 16 16">
  <path fill-rule="evenodd" d="M4 4a4 4 0 1 1 4.5 3.969V13.5a.5.5 0 0 1-1 0V7.97A4 4 0 0 1 4 3.999zm2.493 8.574a.5.5 0 0 1-.411.575c-.712.118-1.28.295-1.655.493a1.319 1.319 0 0 0-.37.265.301.301 0 0 0-.057.09V14l.002.008a.147.147 0 0 0 .016.033.617.617 0 0 0 .145.15c.165.13.435.27.813.395.751.25 1.82.414 3.024.414s2.273-.163 3.024-.414c.378-.126.648-.265.813-.395a.619.619 0 0 0 .146-.15.148.148 0 0 0 .015-.033L12 14v-.004a.301.301 0 0 0-.057-.09 1.318 1.318 0 0 0-.37-.264c-.376-.198-.943-.375-1.655-.493a.5.5 0 1 1 .164-.986c.77.127 1.452.328 1.957.594C12.5 13 13 13.4 13 14c0 .426-.26.752-.544.977-.29.228-.68.413-1.116.558-.878.293-2.059.465-3.34.465-1.281 0-2.462-.172-3.34-.465-.436-.145-.826-.33-1.116-.558C3.26 14.752 3 14.426 3 14c0-.599.5-1 .961-1.243.505-.266 1.187-.467 1.957-.594a.5.5 0 0 1 .575.411z"/>
</svg>`;
        new mapboxgl.Marker(el).setLngLat(post.coordinates).addTo(this.map);
      }
    },
    convertDate: function (dateString) {
      var months = [
        "January",
        "February",
        "March",
        "April",
        "May",
        "June",
        "July",
        "August",
        "September",
        "October",
        "November",
        "December",
      ];
      var date = new Date(dateString);
      return (
        months[date.getMonth()] +
        " " +
        date.getDay() +
        ", " +
        date.getFullYear()
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

hr {
  width: 30%;
}

.desc {
  font-weight: 500;
}
</style>
