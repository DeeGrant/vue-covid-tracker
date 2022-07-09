<template>
  <section class="shadow-md bg-blue-100 p-10 text-center rounded">
    <h3 class="text-3xl text-blue-900 font-bold mb-4">{{label}}</h3>

    <h4 class="text-2xl mb-4">
      <span class="font-bold">New:</span>
      {{numberWithCommas(current)}}
    </h4>
    <h4 class="text-2xl mb-4">
      <span class="font-bold">Total:</span>
      {{numberWithCommas(total)}}
    </h4>
  </section>
</template>

<script>
export default {
  name: 'DataBox',
  props: ['label', 'current', 'total'],
  methods: {
    numberWithCommas(num) {
      return num.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ',')
    }
  }
}
</script>
