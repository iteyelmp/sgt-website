<template>
  <div class="bg-white rounded-xl shadow-md p-6">
    <h3 class="text-2xl font-semibold mb-4 text-gray-800">Your Wallet</h3>
    <div class="space-y-4">
      <p class="text-gray-600">Address: <span class="font-mono">{{ userAddress }}</span></p>
      <p class="text-gray-600">ETH Balance: <span class="font-mono">{{ ethBalance }}</span></p>
      <p class="text-gray-600">SoulQKC Balance: <span class="font-mono">{{ soulBalance }}</span></p>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    userAddress: String,
    ethBalance: String,
    soulBalance: String,
  },
};
</script>

<style scoped>
/* Add any styles for wallet info */
</style>
