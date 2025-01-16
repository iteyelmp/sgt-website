<template>
  <main class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-12">
    <div class="text-center mb-12">
      <h2 class="text-4xl font-bold text-gray-900 mb-4">Soul Gas Token</h2>
      <p class="text-xl text-gray-600 max-w-3xl mx-auto">
        A non-transferable gas token that eliminates entry costs by allowing new users to pay transaction fees without upfront purchases.
      </p>
    </div>

    <div class="grid grid-cols-1 md:grid-cols-2 gap-8 mb-12">
      <wallet-info
          :userAddress="userAddress"
          :ethBalance="ethBalance"
          :soulBalance="soulBalance"
          :totalBalance="totalBalance"
      />
      <div class="bg-white rounded-xl shadow-md p-6">
        <h3 class="text-2xl font-semibold mb-4 text-gray-800">Add the SGT-compatible RPC to Wallet</h3>
        <button
            id="addToken"
            @click="addNetworkToWallet"
            class="w-full bg-purple-600 hover:bg-purple-700 text-white font-semibold py-3 px-4 rounded-lg transition duration-300 mb-4"
        >
          Add the RPC to Metamask
        </button>
        <p class="text-sm text-gray-500">
          Adding the SGT-compatible RPC to MetaMask will display the total balance, which combines both <strong>QKC tokens</strong> and <strong>SGT Tokens</strong>.
        </p>
        <div class="text-sm text-red-500 mt-2">
          <strong>Note:</strong> While the displayed balance reflects the combined total of QKC tokens and SGT tokens, only the QKC token balance is transferable, as SGT tokens are non-transferable and exclusively used for gas fees.
        </div>
      </div>
    </div>

    <key-features />
  </main>
</template>

<script>
import WalletInfo from './WalletInfo.vue';
import KeyFeatures from './KeyFeatures.vue';
import {ethers} from "ethers";

const tokenABI = [
  'function balanceOf(address owner) view returns (uint256)',
];

const RPC = "https://rpc.beta.testnet.l2.quarkchain.io:8545";
const tokenAddress = "0x4200000000000000000000000000000000000800";
const chainId = 3335;
const networkParams = {
  chainId: `0x${chainId.toString(16)}`,
  chainName: 'QuarkChain Special L2 Testnet',
  nativeCurrency: {
    name: 'QKC',
    symbol: 'QKC',
    decimals: 18,
  },
  rpcUrls: ['https://rpc.beta.testnet.l2.quarkchain.io:8645'],
  blockExplorerUrls: [`https://explorer.beta.testnet.l2.quarkchain.io/`],
};

export default {
  components: {
    WalletInfo,
    KeyFeatures,
  },
  data() {
    return {
      ethBalance: '0.0',
      soulBalance: '0.0',
      totalBalance: '0.0'
    };
  },
  props: {
    userAddress: {
      type: String,
      required: true,
      default: 'Not connected',
    },
  },
  watch: {
    userAddress(newAddress) {
      if (newAddress && newAddress !== 'Not connected') {
        this.fetchBalances(newAddress);
      }
    },
  },
  methods: {
    async fetchBalances(address) {
      try {
        const provider = new ethers.JsonRpcProvider(RPC);
        const balance = await provider.getBalance(address);
        this.ethBalance = new Intl.NumberFormat('en-US', {
          minimumFractionDigits: 2,
          maximumFractionDigits: 2
        }).format(parseFloat(ethers.formatEther(balance)));

        // ERC20 Token balance
        const tokenContract = new ethers.Contract(tokenAddress, tokenABI, provider);
        const tokenBalance = await tokenContract.balanceOf(address);
        this.soulBalance = new Intl.NumberFormat('en-US', {
          minimumFractionDigits: 2,
          maximumFractionDigits: 2
        }).format(parseFloat(ethers.formatEther(tokenBalance)));

        const totalBalance = balance + tokenBalance;
        this.totalBalance = new Intl.NumberFormat('en-US', {
          minimumFractionDigits: 2,
          maximumFractionDigits: 2
        }).format(parseFloat(ethers.formatEther(totalBalance)));
      } catch (error) {
        alert('Failed to fetch balances');
      }
    },
    async addNetworkToWallet() {
      try {
        const result = await window.ethereum.request({
          method: 'wallet_addEthereumChain',
          params: [networkParams],
        });
        if (result === null) {
          alert('This network is already added.');
        }
      } catch (error) {
        console.error(error);
        alert('Failed to add network to wallet');
      }
    },
  },
  mounted() {
    if (this.userAddress && this.userAddress !== 'Not connected') {
      this.fetchBalances(this.userAddress);
    }
  },
};
</script>

<style scoped>
/* Add any styles for main content */
</style>
