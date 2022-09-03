<script lang="ts">
import ColumnChart from '../components/amchart/ColumnChart.vue';
import { defineComponent } from '@vue/runtime-core';
import { computed } from "vue";


// const users = [
//   {name: 'Jhon Doe a',age: 'string'},
//   {name: 'Jhon Doe b',age: 25},
//   {name: 'Jhon Doe b',age: 30},
//   {name: 'Jhon Doe c',age: 20},
// ];

export default defineComponent({

components: {
  ColumnChart,

},
 setup() {
 
    const chartSeries = computed(() => [
    {
      name: "Question(s)",
      data:  [3, 2,4, 1],
    },
  ]);
 

return {
    chartSeries
  }
 },

});
</script>


<template>
  <div class="tw-mt-8" style="width: 80%" >
    <h1>XY Column Chart</h1>
    <ColumnChart  />
  </div>
</template>

<!-- <template>
  <div id="chart" >
    <CohortContentViews height="400" :series="series" :options="chartOptions" />
  </div>
</template> -->



