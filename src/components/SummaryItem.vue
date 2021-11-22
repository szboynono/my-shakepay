<script setup lang="ts">
defineProps<{
  item: {
    currency: string,
    balance: number,
    price: number,
    amount: number
  }
}>()
</script>

<template>
  <div class="flex flex-row justify-between">
    <img src="../assets/icons/currency-cad.svg" alt="cad" />
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
