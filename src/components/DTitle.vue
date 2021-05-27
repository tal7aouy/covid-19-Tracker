<template>
  <div class="text-center">
    <h3 class="text-3xl font-semibold">{{ text }}</h3>
    <div class="text-2xl mt-4 mb-10">
      {{ timestamp }}
    </div>
  </div>
</template>

<script>
import moment from 'moment'
export default {
  name: 'DTitle',
  props: ['text', 'dataDate'],
  computed: {
    timestamp() {
      return moment(this.dataDate).format('MMMM Do YYYY, h:mm:ss a')
    },
  },
}
</script>

<style></style>
