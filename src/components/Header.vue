<script setup lang="ts">
defineProps<{
  balance: string
}>()
</script>

<template>
  <header>
    <img class="mx-auto mt-4 mb-2" src="../assets/icons/logo.svg" alt="shakepay">
    <p class="text-center mb-4">$ {{ balance }}</p>
    <hr>
  </header>
</template>

<style>
</style>
