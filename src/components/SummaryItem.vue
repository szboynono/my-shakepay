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
  return new URL(`../assets/icons/currency-${props.item.currency.toLowerCase()}.svg`, import.meta.url);
})

</script>

<template>
  <div class="flex flex-row justify-between">
    <img :src="iconPath" alt="cad" />
    <div>
      <h3>Dollar</h3>
      <div>$ {{item.price}}</div>
    </div>
    <div>
      <div>{{ item.amount }}</div>
      <div>$ {{ item.balance }}</div>
    </div>
  </div>
</template>

<style>
</style>
