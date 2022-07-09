<template>
  <main v-if="!loading">
    <DataTitle :text="title" :data-date="dataDate"></DataTitle>

    <DataBoxes :stats="stats"></DataBoxes>

    <CountrySelect @get-country="setStats" :countries="countries"></CountrySelect>

    <button
        @click="setGlobalStats"
        v-if="stats.Country"
        class="bg-green-700 text-white rounded p-3 mt-10 focus:outline-none hover:bg-green-600">View Global Summary</button>
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
import CountrySelect from "@/components/CountrySelect";

export default {
  name: 'HomeView',
  components: {
    DataBoxes,
    DataTitle,
    CountrySelect
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
    },
    setStats(country) {
      this.stats = country
      this.title = country.Country
    },
    async setGlobalStats() {
      this.loading = true

      const data = await this.fetchCovidData()
      this.title = 'Global'
      this.stats = data.Global

      this.loading = false
    }
  },
  async created() {
    const data = await this.fetchCovidData()
    this.dataDate = data.Date
    this.stats = data.Global
    this.countries = data.Countries

    this.loading = false
  }
}
</script>
