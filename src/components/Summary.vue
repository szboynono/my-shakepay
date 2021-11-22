<script setup lang="ts">
import SummaryItemVue from './SummaryItem.vue';

defineProps<{
  items: {
    currency: string,
    balance: number,
    price: number,
    amount: number
  }[]
}>()
</script>

<template>
  <ul>
    <li v-for="item in items">
          <SummaryItemVue :item="item" />
    </li>
  </ul>
</template>

<style>
</style>
