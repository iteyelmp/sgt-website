<template>
  <nav class="bg-white shadow-sm">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
      <div class="flex justify-between h-16">
        <div class="flex items-center">
          <img class="logo" src="@/assets/logo.png" />
        </div>
        <div class="flex items-center">
          <div v-if="address" class="text-gray-400 break-all">
            {{ address }}
          </div>
          <button
              v-else
              id="connectWallet"
              @click="connectWallet"
              class="bg-blue-600 hover:bg-blue-700 text-white font-semibold py-2 px-4 rounded-lg transition duration-300"
          >
            Connect Wallet
          </button>
        </div>
      </div>
    </div>
  </nav>
</template>

<script>

export default {
  data() {
    return {
      address: null,
    };
  },
  methods: {
    async connectWallet() {
      try {
        if (window.ethereum) {
          window.ethereum
              .request({method: "eth_requestAccounts"})
              .then((accounts) => {
                // account
                if (accounts.length === 0) {
                  alert("MetaMask is locked or the user has not connected any accounts");
                  return;
                }
                const address = accounts[0];
                this.address = `${address.substring(0, 6)}...${address.substring(38)}`;
                this.$emit('walletConnected', {
                  address: address,
                });
                this.walletConnected = true;
              })
              .catch(() => {
                alert('Failed to connect wallet');
              });
        }
      } catch (error) {
        console.error(error);
        alert('Failed to connect wallet');
      }
    },
  },
};
</script>

<style scoped>
.logo {
  height: 32px;
}
</style>
