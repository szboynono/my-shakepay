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
        <router-link :to="'/details/' + item.currency">
          <SummaryItemVue :item="item" />
        </router-link>
    </li>
  </ul>
</template>

<style>
</style>
