<script setup lang="ts">
import SummaryItemVue from './SummaryItem.vue';

defineProps<{
  items: any[]
}>()
</script>

<template>
  <ul>
    <li v-for="item in items">
          <SummaryItemVue />
    </li>
  </ul>
</template>

<style>
</style>
