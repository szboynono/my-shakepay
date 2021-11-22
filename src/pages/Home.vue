<script setup lang="ts">
import { computed, onMounted, ref } from 'vue';
import Header from '../components/Header.vue'
import Summary from '../components/Summary.vue';
import axios from 'axios';

const transactionsData = ref();
const rateData = ref();
const summaryItemsData = computed(() => {
  return [{
    currency: 'btc',
    balance: 0,
    price: 123,
    amount: 0.444
  }]
})

const balance = computed(() => {
  let sum = 0;
  if (transactionsData.value && rateData.value) {
    transactionsData.value.forEach((item: any) => {
      let currAmount = 0;
      if (item.currency && item.currency !== 'CAD') {

        const exchangeName = `${item.currency}_CAD`;

        if (exchangeName) {
          const rateToCad = rateData.value[exchangeName];
          currAmount = item.amount * rateToCad;
        }
      } else if (item.currency === 'CAD') {
        currAmount = item.amount
      }

      if (item.direction === 'credit') {
        sum += currAmount;
      } else if (item.direction === 'debit') {
        sum -= currAmount;
      }
    });
  }

  return sum.toFixed(0);
})

onMounted(() => {
  axios.get('https://shakepay.github.io/programming-exercise/web/rates.json').then(res => {
    rateData.value = res.data;
  })

  axios.get('https://shakepay.github.io/programming-exercise/web/transaction_history.json').then(res => {
    transactionsData.value = res.data;
  });
})

</script>

<template>
  <Header :balance="balance" />
  <Summary :items="summaryItemsData" />
</template>

<style>
</style>
