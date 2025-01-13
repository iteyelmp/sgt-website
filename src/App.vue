<template>
  <div>
    <Navbar @walletConnected="walletConnected" />
    <main-content
        :userAddress="userAddress"
        :ethBalance="ethBalance"
        :soulBalance="soulBalance"
    />
  </div>
</template>

<script>
import Navbar from './components/NavBar.vue';
import MainContent from './components/MainContent.vue';

export default {
  components: {
    Navbar,
    MainContent,
  },
  data() {
    return {
      userAddress: 'Not connected',
      ethBalance: '0.0',
      soulBalance: '0.0',
    };
  },
  methods: {
    walletConnected(data) {
      this.userAddress = data.address;
      this.ethBalance = '100.0'; // Replace with actual logic to fetch balance
      this.soulBalance = '1000.0'; // Simulate SoulQKC balance
    },
  },
};
</script>

<style>
@import "https://cdn.jsdelivr.net/npm/tailwindcss@2.2.19/dist/tailwind.min.css";
</style>
