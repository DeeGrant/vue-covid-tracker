<template>
  <section class="grid md:grid-cols-2 gap-4">
    <DataBox :label="'Cases'" :current="stats.NewConfirmed" :total="stats.TotalConfirmed"></DataBox>
    <DataBox :label="'Deaths'" :current="stats.NewDeaths" :total="stats.TotalDeaths"></DataBox>
  </section>
</template>

<script>
import DataBox from "@/components/DataBox";

export default {
  name: 'DataBoxes',
  props: ['stats'],
  components: {DataBox}
}
</script>
