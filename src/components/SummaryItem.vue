<script setup lang="ts">
import { computed, ref } from 'vue';

const props = defineProps<{
  item: {
    currency: string,
    balance: number,
    price: number,
    amount: number
  }
}>()

const iconPath = computed(() => {
  const url = new URL(`../assets/icons/currency-${props.item.currency.toLowerCase()}.svg`, import.meta.url);
  return '' + url;
})

</script>

<template>
  <div class="my-3 flex flex-row justify-between">
    <img :src="iconPath" alt="cad" />
    <div>
      <h3>{{ item.currency }}</h3>
      <div v-if="item.currency !== 'CAD'">$ {{item.price}}</div>
    </div>
    <div>
      <div>{{ item.amount }}</div>
      <div v-if="item.currency !== 'CAD'">$ {{ item.balance }}</div>
    </div>
  </div>
</template>

<style>
</style>
