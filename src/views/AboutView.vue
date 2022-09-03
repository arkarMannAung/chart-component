<script setup lang="ts">
// @ts-ignore
import ChartComponent from '@/components/ChartComponent.vue';
import { defineComponent } from '@vue/runtime-core';
const users = [
  {name: 'Jhon Doe a',age: 'string'},
  {name: 'Jhon Doe b',age: 25},
  {name: 'Jhon Doe b',age: 30},
  {name: 'Jhon Doe c',age: 20},
];
</script>

<template>
  <div class="about">
    <h1>This is an about page</h1>
    <ChartComponent :users="users" />
  </div>
</template>
