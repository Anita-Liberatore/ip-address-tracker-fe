<template>
  <div class="flex flex-col h-screen max-h-screen">
    <!-- Search / Results -->
    <div class="z-20 flex justify-center relative bg-hero-pattern bg-cover px-4 pt-8 pb-32">
      <!-- Search Input -->
      <div class="w-full max-w-screen-sm input-part">
        <h1 class="text-white text-center text-3xl pb-4 text-ip-address">{{textLabelIpAddressTracker}}</h1>
        <div class="flex">
          <input v-model="queryIpInput"
            class="input-text flex-1 py-3 px-2 rounded-tl-md rounded-bl-md focus:outline-none" type="text"
            placeholder="Search for any IP address or domain">
          <i @click="getIpInfo"
            class="cursor-pointer bg-black text-white px-4 rounded-tr-md rounded-br-md flex items-center fas fa-chevron-right"></i>
        </div>
      </div>

      <!-- IP info -->
      <IPInfoDetail v-if="ipInfo" :ipInfo="ipInfo" />

    </div>
    <!--Map-->
    <div id="mapid" class="h-full z-10"></div>
  </div>
</template>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Rubik:wght@300;400&display=swap');

body {
  font-family: 'Rubik', sans-serif;
}

.text-ip-address {
  font-weight: 600;
}

i:hover {
  background-color: hsl(0, 0%, 17%)
}
/* Media Queries */
@media only screen and (max-width: 700)  {

  .input-part {
    width: 90%;
  }

  ::-webkit-input-placeholder {
    /* Edge */
    font-size: 14px;
  }

  :-ms-input-placeholder {
    /* Internet Explorer 10-11 */
    font-size: 14px;
  }

  ::placeholder {
    font-size: 14px;
  }
}



</style>


<script>
import IPInfoDetail from "../components/IpInfoDetail.vue"
import leaflet from "leaflet"
import { onMounted, ref } from "vue";
import axios from "axios"

export default {
  name: 'HomeView',
  components: {
    IPInfoDetail
  },

  setup() {
    let map;
    const queryIpInput = ref("");
    const ipInfo = ref(null)
    onMounted(() => {

      ipInfo.value = {
        address: "192.212.174.101",
        state: "California",
        city: "South San Gabriel, California, US",
        timezone: "-07:00",
        isp: "Google LLC",
        lat: "34.04915",
        lng: "-118.09462"
      };

      map = leaflet.map('mapid').setView([34.04915, -118.09462], 12);

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
        .addTo(map);
    });


    const getIpInfo = async () => {
      try {
        const data = await axios.get(`https://geo.ipify.org/api/v2/country,city?apiKey=at_fqIAQzAS7f1S8ojLlIB5WUCGg8rcK&ipAddress=${queryIpInput.value}`)
        const result = data.data
        ipInfo.value = {
          address: result.ip,
          city: result.location.city + ", " + result.location.country,
          timezone: result.location.timezone,
          isp: result.isp,
          lat: result.location.lat,
          lng: result.location.lng
        };

        map.setView([ipInfo.value.lat, ipInfo.value.lng], 12);
        queryIpInput.value = ""
      } catch (err) {
        alert(err.message)
      }
    }
    return { queryIpInput, ipInfo, getIpInfo }

  },

  data() {
    return {
      textLabelIpAddressTracker: 'IP Address Tracker'
    }
  }
}
</script>

