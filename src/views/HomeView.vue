<template>
  <main v-if="!loading">
    <DataTitle :text="title" :data-date="dataDate"></DataTitle>

    <DataBoxes :stats="stats"></DataBoxes>
  </main>
  <main class="flex flex-col align-center justify-center text-center" v-else>
    <div class="text-gray-500 text-3xl mt-10 mb-6">
      Fetching Data...
    </div>
    <img :src="loadingImage" class="w-24 m-auto" alt="hourglass">
  </main>
</template>

<script>
import DataTitle from "@/components/DataTitle";
import DataBoxes from "@/components/DataBoxes";

export default {
  name: 'HomeView',
  components: {
    DataBoxes,
    DataTitle
  },
  data() {
    return {
      loading: true,
      title: 'Global',
      dataDate: '',
      stats: {},
      countries: [],
      loadingImage: require('../assets/hourglass.gif')
    }
  },
  methods: {
    async fetchCovidData() {
      const res = await fetch('https://api.covid19api.com/summary')
      return await res.json()
    }
  },
  async created() {
    const data = await this.fetchCovidData()
    console.log(data)
    this.dataDate = data.Date
    this.stats = data.Global
    this.countries = data.Countries.map(data => data.Country)
    console.log(this.countries)
    this.loading = false
  }
}
</script>
