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


        </div>
      </div>

    </div>

  </div>
</template>

<style>
  .text-ip-address {
    font-weight: 600;
  }
</style>


<script>


export default {
  name: 'HomeView',
  components: {

  },

  data() {
    return {
      textLabelIpAddressTracker: 'IP Address Tracker'
    }
  }
}
</script>

