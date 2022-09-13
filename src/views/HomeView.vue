<template>
  <div class="flex flex-col h-screen max-h-screen">
    <!-- Search / Results -->
    <div class="z-20 flex justify-center relative bg-hero-pattern bg-cover px-4 pt-8 pb-32">
      <!-- Search Input -->
      <div class="w-full max-w-screen-sm">
        <h1 class="text-white text-center text-3xl pb-4 text-ip-address">{{textLabelIpAddressTracker}}</h1>
        <div class="flex">
          <input class="flex-1 py-3 px-2 rounded-tl-md rounded-bl-md focus:outline-none" type="text"
            placeholder="Search for any IP address or leave empty to get your ip info">
          <i
            class="cursor-pointer bg-black text-white px-4 rounded-tr-md rounded-br-md flex items-center fas fa-chevron-right"></i>
        </div>
      </div>

      <!-- IP info -->
      <IPInfoDetail />

    </div>
    <!--Map-->
    <div id="mapid" class="h-full z-10"></div>
  </div>
</template>

<style>
.text-ip-address {
  font-weight: 600;
}
</style>


<script>
import IPInfoDetail from "../components/IpInfoDetail.vue"
import leaflet from "leaflet"
import { onMounted } from "vue";

export default {
  name: 'HomeView',
  components: {
    IPInfoDetail
  },

  setup() {
    let mymap;

    onMounted(() => {
      mymap = leaflet.map('mapid').setView([51.505, -0.09], 13);

      leaflet
        .tileLayer(
          "https://api.mapbox.com/styles/v1/{id}/tiles/{z}/{x}/{y}?access_token=pk.eyJ1IjoiYW5pdGFsaWJlcmF0b3JlIiwiYSI6ImNsODAxZ3JlZjAxdGszcnQ5OWMxOGl2aWoifQ.nXYktS1QcKh2aZAOG5e1zg",
          {
            attribution:
              'Map data &copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors, Imagery © <a href="https://www.mapbox.com/">Mapbox</a>',
            maxZoom: 18,
            id: "mapbox/streets-v11",
            tileSize: 512,
            zoomOffset: -1,
            accessToken:
              "pk.eyJ1IjoiYW5pdGFsaWJlcmF0b3JlIiwiYSI6ImNsODAxZ3JlZjAxdGszcnQ5OWMxOGl2aWoifQ.nXYktS1QcKh2aZAOG5e1zg",
          }
        )
        .addTo(mymap);
    });

  },

  data() {
    return {
      textLabelIpAddressTracker: 'IP Address Tracker'
    }
  }
}
</script>

