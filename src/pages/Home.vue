<script setup lang="ts">
import { computed, onMounted, ref } from 'vue';
import Header from '../components/Header.vue'
import Summary from '../components/Summary.vue';
import axios from 'axios';

const transactionsData = ref();
const rateData = ref();

const constructItem = (currData: any, currency: string) => {
  let currAmount = 0;
  let balance = 0;
  let price = 0;
  const exchangeName = `${currency}_CAD`;
  const rateToCad = rateData.value[exchangeName];
  price = rateToCad;
  currData.forEach((data: any) => {
    if (data.direction === 'credit') {
      balance += data.amount * rateToCad;
      currAmount += data.amount;
    } else if (data.direction === 'debit') {
      balance -= data.amount * rateToCad;
      currAmount -= data.amount;
    }
  });

  return {
    currency,
    balance: balance.toFixed(0),
    price,
    amount: currAmount.toFixed(0)
  }
}

const summaryItemsData = computed(() => {
  const items: any = [];

  if (transactionsData.value && rateData.value) {
    const btcData = transactionsData.value.filter((data: any) => data.currency === 'BTC');
    const finalBtcData = constructItem(btcData, 'BTC');
    items.push(finalBtcData)

    const ethData = transactionsData.value.filter((data: any) => data.currency === 'ETH');
    const finalEthData = constructItem(ethData, 'ETH');
    items.push(finalEthData)

    const cadData = transactionsData.value.filter((data: any) => data.currency === 'CAD');
    const finalCadData = constructItem(cadData, 'CAD');
    items.push(finalCadData)
  }
  return items;
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
