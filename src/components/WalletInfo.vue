<template>
  <div class="bg-white rounded-xl shadow-md p-6">
    <h3 class="text-2xl font-semibold mb-4 text-gray-800">Your Wallet</h3>
    <div class="space-y-4">
      <p class="text-black">Address: <span class="font-mono text-gray-500 ml-2">{{ userAddress }}</span></p>
      <p class="text-black">QKC Balance: <span class="font-mono text-gray-500 ml-2">{{ ethBalance }}</span></p>
      <p class="text-black">Soul Gas Token Balance: <span class="font-mono text-gray-500 ml-2">{{ soulBalance }}</span></p>
      <p class="text-black">Total Balance: <span class="font-mono text-gray-500 ml-2">{{ totalBalance }}</span></p>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    userAddress: String,
    ethBalance: String,
    soulBalance: String,
    totalBalance: String,
  },
};
</script>

<style scoped>
/* Add any styles for wallet info */
</style>
