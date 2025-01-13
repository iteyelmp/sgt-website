<template>
  <nav class="bg-white shadow-sm">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
      <div class="flex justify-between h-16">
        <div class="flex items-center">
          <img class="logo" src="@/assets/logo.png" />
        </div>
        <div class="flex items-center">
          <button
              id="connectWallet"
              @click="connectWallet"
              class="bg-blue-600 hover:bg-blue-700 text-white font-semibold py-2 px-4 rounded-lg transition duration-300"
          >
            {{ walletConnected ? 'Connected' : 'Connect Wallet' }}
          </button>
        </div>
      </div>
    </div>
  </nav>
</template>

<script>
// import {ethers} from "ethers";

export default {
  data() {
    return {
      walletConnected: false,
    };
  },
  methods: {
    async connectWallet() {
      // try {
      //   if (typeof window.ethereum !== 'undefined') {
      //     const provider = new Web3Provider(window.ethereum);
      //     await window.ethereum.request({ method: 'eth_requestAccounts' });
      //     const signer = await provider.getSigner();
      //     const address = await signer.getAddress();
      //     this.$emit('walletConnected', {
      //       address: `${address.substring(0, 6)}...${address.substring(38)}`,
      //     });
      //     this.walletConnected = true;
      //   }
      // } catch (error) {
      //   console.error(error);
      //   alert('Failed to connect wallet');
      // }
    },
  },
};
</script>

<style scoped>
.logo {
  padding: 10px 0;
}
</style>
