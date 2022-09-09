<template>
  <div class="flex flex-col h-screen max-h-screen">
    <!-- Search / Results -->
    <div
      class="z-20 flex justify-center relative bg-hero-pattern bg-cover px-4 pt-8 pb-32"
    >
      <!-- Search Input -->
      <div class="w-full max-w-screen-sm">
        <h1 class="text-white text-center text-3xl pb-4 text-ip-address">{{textLabelIpAddressTracker}}</h1>
        <div class="flex">
          <input class="flex-1 py-3 px-2 rounded-tl-md rounded-bl-md focus:outline-none" type="text" placeholder="Search for any IP address or leave empty to get your ip info">
          <i class="cursor-pointer bg-black text-white px-4 rounded-tr-md rounded-br-md flex items-center fas fa-chevron-right"></i>
        </div>
      </div>

      <!-- IP info -->
      <IPInfoDetail/>

    </div>

  </div>
</template>

<style>
  .text-ip-address {
    font-weight: 600;
  }
</style>


<script>
import IPInfoDetail from "../components/IpInfoDetail.vue"

export default {
  name: 'HomeView',
  components: {
    IPInfoDetail
  },

  data() {
    return {
      textLabelIpAddressTracker: 'IP Address Tracker'
    }
  }
}
</script>

