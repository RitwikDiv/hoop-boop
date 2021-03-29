<template>
  <form>
    <br />
    <div v-html="getPostStatus"></div>
    <div class="form-group">
      <label for="memory-title"><strong>Title</strong></label>
      <input
        type="text"
        class="form-control"
        id="memory-title"
        v-model="memory.title"
        placeholder="Enter the title of your memory"
        required
      />
    </div>
    <div class="form-group">
      <label for="memory-location"><strong>Location</strong></label>
      <input
        type="text"
        class="form-control"
        id="memory-location"
        v-model="memory.location_desc"
        placeholder="Enter the location of the memory"
        required
      />
    </div>
    <div class="form-group">
      <label for="memory-date"><strong>Date</strong></label>
      <input
        type="date"
        class="form-control"
        v-model="memory.date"
        id="memory-date"
        required
      />
    </div>
    <div class="form-group">
      <label for="memory-desc"> <strong>Description</strong></label>
      <textarea
        class="form-control"
        id="memory-desc"
        rows="3"
        v-model="memory.desc"
        placeholder="What happened?"
        required
      />
    </div>
    <button type="button" class="btn btn-dark mt-2" @click="handleSubmitForm">
      <strong>Submit</strong>
    </button>
  </form>
</template>

<script>
const axios = require("axios");

export default {
  name: "MemoryCreate",
  methods: {
    async handleSubmitForm() {
      const locationString = encodeURIComponent(this.memory.location_desc);
      const geocodeUrl = `https://api.mapbox.com/geocoding/v5/mapbox.places/${locationString}.json?types=poi&limit=1&access_token=${this.apiKey}`;
      await axios
        .get(geocodeUrl)
        .then((res) => {
          this.memory.location_desc = res.data.features[0].text;
          this.memory.coordinates = res.data.features[0].center;
          this.postStatus = "success";
        })
        .catch((error) => {
          console.log(error);
          this.postStatus = "failure";
        });
      console.log(this.memory);
      this.memory = {
        title: "",
        desc: "",
        location_desc: "",
        date: "",
        coordinates: [],
      };
    },
  },
  data() {
    return {
      apiKey:
        "pk.eyJ1Ijoicml0d2lrZGl2IiwiYSI6ImNrbXQ3dzB5OTBwNjAycG54b2FqM2J5N2gifQ.bVO6sXRv29Y6d57cicHUOg",
      postStatus: "unknown",
      memory: {
        title: "",
        desc: "",
        location_desc: "",
        date: "",
        coordinates: [],
      },
    };
  },
  computed: {
    getPostStatus() {
      if (this.postStatus == "unknown") {
        return ``;
      } else if (this.postStatus == "success") {
        return `<div class="alert alert-success" role="alert">
      <svg
        xmlns="http://www.w3.org/2000/svg"
        width="20"
        height="20"
        fill="currentColor"
        class="bi bi-geo-fill mr-3"
        viewBox="0 0 16 16"
      >
        <path
          fill-rule="evenodd"
          d="M4 4a4 4 0 1 1 4.5 3.969V13.5a.5.5 0 0 1-1 0V7.97A4 4 0 0 1 4 3.999zm2.493 8.574a.5.5 0 0 1-.411.575c-.712.118-1.28.295-1.655.493a1.319 1.319 0 0 0-.37.265.301.301 0 0 0-.057.09V14l.002.008a.147.147 0 0 0 .016.033.617.617 0 0 0 .145.15c.165.13.435.27.813.395.751.25 1.82.414 3.024.414s2.273-.163 3.024-.414c.378-.126.648-.265.813-.395a.619.619 0 0 0 .146-.15.148.148 0 0 0 .015-.033L12 14v-.004a.301.301 0 0 0-.057-.09 1.318 1.318 0 0 0-.37-.264c-.376-.198-.943-.375-1.655-.493a.5.5 0 1 1 .164-.986c.77.127 1.452.328 1.957.594C12.5 13 13 13.4 13 14c0 .426-.26.752-.544.977-.29.228-.68.413-1.116.558-.878.293-2.059.465-3.34.465-1.281 0-2.462-.172-3.34-.465-.436-.145-.826-.33-1.116-.558C3.26 14.752 3 14.426 3 14c0-.599.5-1 .961-1.243.505-.266 1.187-.467 1.957-.594a.5.5 0 0 1 .575.411z"
        />
      </svg>
      <strong>Thank you for sharing your memory!</strong>
    </div>`;
      } else {
        return `<div class="alert alert-danger" role="alert">
      <svg
        xmlns="http://www.w3.org/2000/svg"
        width="20"
        height="20"
        fill="currentColor"
        class="bi bi-geo-fill mr-3"
        viewBox="0 0 16 16"
      >
        <path
          fill-rule="evenodd"
          d="M4 4a4 4 0 1 1 4.5 3.969V13.5a.5.5 0 0 1-1 0V7.97A4 4 0 0 1 4 3.999zm2.493 8.574a.5.5 0 0 1-.411.575c-.712.118-1.28.295-1.655.493a1.319 1.319 0 0 0-.37.265.301.301 0 0 0-.057.09V14l.002.008a.147.147 0 0 0 .016.033.617.617 0 0 0 .145.15c.165.13.435.27.813.395.751.25 1.82.414 3.024.414s2.273-.163 3.024-.414c.378-.126.648-.265.813-.395a.619.619 0 0 0 .146-.15.148.148 0 0 0 .015-.033L12 14v-.004a.301.301 0 0 0-.057-.09 1.318 1.318 0 0 0-.37-.264c-.376-.198-.943-.375-1.655-.493a.5.5 0 1 1 .164-.986c.77.127 1.452.328 1.957.594C12.5 13 13 13.4 13 14c0 .426-.26.752-.544.977-.29.228-.68.413-1.116.558-.878.293-2.059.465-3.34.465-1.281 0-2.462-.172-3.34-.465-.436-.145-.826-.33-1.116-.558C3.26 14.752 3 14.426 3 14c0-.599.5-1 .961-1.243.505-.266 1.187-.467 1.957-.594a.5.5 0 0 1 .575.411z"
        />
      </svg>
      <strong>Unable to share your memory. Please fill the form properly.</strong>
    </div>`;
      }
    },
  },
};
</script>


<style>
</style>
