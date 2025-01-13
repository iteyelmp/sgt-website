<template>
  <main class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-12">
    <div class="text-center mb-12">
      <h2 class="text-4xl font-bold text-gray-900 mb-4">SoulQKC Gas Token</h2>
      <p class="text-xl text-gray-600 max-w-3xl mx-auto">
        A non-transferable gas token that eliminates entry costs by allowing new users to pay transaction fees without upfront purchases.
      </p>
    </div>

    <div class="grid grid-cols-1 md:grid-cols-2 gap-8 mb-12">
      <wallet-info
          :userAddress="userAddress"
          :ethBalance="ethBalance"
          :soulBalance="soulBalance"
      />
      <div class="bg-white rounded-xl shadow-md p-6">
        <h3 class="text-2xl font-semibold mb-4 text-gray-800">Add to Wallet</h3>
        <button
            id="addToken"
            @click="addTokenToWallet"
            class="w-full bg-purple-600 hover:bg-purple-700 text-white font-semibold py-3 px-4 rounded-lg transition duration-300 mb-4"
        >
          Add SoulQKC to Wallet
        </button>
        <p class="text-sm text-gray-500">
          Add SoulQKC token to your wallet to track your balance easily.
        </p>
      </div>
    </div>

    <key-features />
  </main>
</template>

<script>
import WalletInfo from './WalletInfo.vue';
import KeyFeatures from './KeyFeatures.vue';

export default {
  components: {
    WalletInfo,
    KeyFeatures,
  },
  data() {
    return {
      userAddress: 'Not connected',
      ethBalance: '0.0',
      soulBalance: '0.0',
    };
  },
  methods: {
    async addTokenToWallet() {
      try {
        const tokenAddress = '0x0000000000000000000000000000000000000000'; // Replace with actual token address
        const tokenSymbol = 'SoulQKC';
        const tokenDecimals = 18;

        const wasAdded = await window.ethereum.request({
          method: 'wallet_watchAsset',
          params: {
            type: 'ERC20',
            options: {
              address: tokenAddress,
              symbol: tokenSymbol,
              decimals: tokenDecimals,
            },
          },
        });

        if (wasAdded) {
          alert('Token was successfully added to your wallet!');
        }
      } catch (error) {
        console.error(error);
        alert('Failed to add token to wallet');
      }
    },
    walletConnected(data) {
      this.userAddress = data.address;
      this.ethBalance = '100.0'; // Replace with actual logic to fetch balance
      this.soulBalance = '1000.0'; // Simulate SoulQKC balance
    },
  },
};
</script>

<style scoped>
/* Add any styles for main content */
</style>
