<template>
  <div class="bg-white rounded-xl shadow-md p-6">
    <h3 class="text-2xl font-semibold mb-4 text-gray-800">Add to Wallet</h3>
    <button
        @click="addTokenToWallet"
        class="w-full bg-purple-600 hover:bg-purple-700 text-white font-semibold py-3 px-4 rounded-lg transition duration-300 mb-4">
      Add SoulQKC to Wallet
    </button>
    <p class="text-sm text-gray-500">
      Add SoulQKC token to your wallet to track your balance easily.
    </p>
  </div>
</template>

<script>
export default {
  methods: {
    addTokenToWallet() {
      this.$emit('add-token');
    },
  },
};
</script>
