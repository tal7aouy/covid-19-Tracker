<template>
  <div class="grid md:grid-cols-2 gap-4">
    <div class="shadow-md bg-indigo-200 p-10 text-center rounded-sm">
      <h3 class="text-3xl text-indigo-900 font-semibold mb-3">Cases</h3>
      <div class="text-2xl mb-3">
        <span class="font-semibold">New:</span>
        {{ getNumberWithCommas(stats.NewConfirmed) }}
        <br />
        <span class="font-semibold">Total</span>
        {{ getNumberWithCommas(stats.TotalConfirmed) }}
      </div>
    </div>
    <div class="shadow-md bg-indigo-300 p-10 text-center rounded-sm">
      <h3 class="text-3xl text-indigo-900 font-semibold mb-3">Deaths</h3>
      <div class="text-2xl mb-3">
        <span class="font-semibold">New:</span>
        {{ getNumberWithCommas(stats.NewDeaths) }}
        <br />

        <span class="font-semibold">Total</span>
        {{ getNumberWithCommas(stats.TotalDeaths) }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'DBoxes',
  props: ['stats'],
  methods: {
    getNumberWithCommas(num) {
      return num.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ',')
    },
  },
}
</script>

<style></style>
