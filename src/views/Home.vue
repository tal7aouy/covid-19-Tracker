<template>
  <main v-if="!loading">
    <d-title v-bind="{ text: title, dataDate: dataDate }" />
    <d-boxes :stats="stats" />
    <SelectCountry :countries="countries" @get-country="getCountryInfo" />
    <button
      v-if="stats.Country"
      class="bg-indigo-400 text-white rounded p-2 mt-10 focus:outline-none hover:bg-indigo-400"
      @click="clearCountry"
    >
      Clear Country
    </button>
  </main>
  <main class="flex flex-col items-center  justify-center" v-else>
    <div class="text-gray-500 text-3xl mt-10 mb-6">
      Loading Data
      <img :src="loadingGif" class="w-24 mt-3 m-auto" alt="loading now" />
    </div>
  </main>
</template>

<script>
import DTitle from '@/components/DTitle'
import DBoxes from '@/components/DBoxes'
import SelectCountry from '@/components/SelectCountry'
export default {
  name: 'Home',
  components: {
    DTitle,
    DBoxes,
    SelectCountry,
  },
  data() {
    return {
      title: 'Global',
      loading: true,
      dataDate: '',
      stats: {},
      countries: [],
      loadingGif: require('../assets/loading.gif'),
    }
  },
  methods: {
    async getCovidData() {
      const response = await fetch('https://api.covid19api.com/summary')
      const data = response.json()
      return data
    },
    getCountryInfo(country) {
      this.stats = country
      this.title = country.Country
    },
    async clearCountry() {
      this.loading = true
      const data = await this.getCovidData()
      this.title = 'Global'
      this.stats = data.Global
      this.loading = false
    },
  },
  async created() {
    const data = await this.getCovidData()
    // init data
    this.dataDate = data.Date
    this.stats = data.Global
    this.countries = data.Countries

    this.loading = false
  },
}
</script>
