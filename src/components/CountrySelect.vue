<template>
  <select
      @change="onChange()"
      v-model="selected"
      class="form-select mt-10 block w-full border p-3 rounded"
  >
    <option v-for="country in countries" :value="country.ID">{{country.Country}}</option>
  </select>
</template>

<script>
export default {
  name: 'CountrySelect',
  props: ['countries'],
  data() {
    return {
      selected: 0
    }
  },
  methods: {
    onChange() {
      const country = this.countries.find(c => c.ID === this.selected)
      this.$emit('get-country', country)
    }
  }
}
</script>
