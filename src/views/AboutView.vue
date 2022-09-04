<script setup lang="ts">
// @ts-ignore
import ColumnChart from '../components/amchart/ColumnChart.vue';
// @ts-ignore
import ColumnChartRevise from '../components/amchart/ColumnChartRevise.vue';
import { onMounted } from 'vue';
const category = [
  { category: 'dart', value: 50 },
  { category: 'php', value: 33 },
  { category: 'javascript', value: 50 },
  { category: 'python', value: 34 },
];
const today = new Date();
const next = new Date();
const date = [
  { date: next.setDate(today.getDate() + 1), value: 26 },
  { date: next.setDate(today.getDate() + 2), value: 60 },
  { date: next.setDate(today.getDate() + 3), value: 57 },
  { date: next.setDate(today.getDate() + 4), value: 45 },
  { date: next.setDate(today.getDate() + 5), value: 90 },
  { date: next.setDate(today.getDate() + 6), value: 60 },
  { date: next.setDate(today.getDate() + 7), value: 20 }
];
</script>


<template>
  <div class="tw-mt-8" style="width: 80%" >
    <h1>XY Column Chart</h1>
    <!-- <ColumnChart  /> -->
    <ColumnChartRevise 
      :datas="category" 
      uniqueId="category"
      width="100%"
      height="30px"
    />
    <ColumnChartRevise 
      :datas="date" 
      uniqueId="date" 
      timeUnit="month"
      width="100%"
      height="300px"
    />
  </div>
</template>



