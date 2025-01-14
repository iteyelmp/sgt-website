<template>
  <div>
    <Navbar @walletConnected="walletConnected" />
    <main-content :userAddress="userAddress" />
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
    },
  },
};
</script>

<style>
@import "https://cdn.jsdelivr.net/npm/tailwindcss@2.2.19/dist/tailwind.min.css";
</style>
