<template>
  <div class="bg-white rounded-xl shadow-md p-6">
    <h3 class="text-2xl font-semibold mb-4 text-gray-800">Your Wallet</h3>
    <div class="space-y-4">
      <p class="text-black">Address: <span class="font-mono text-gray-500 ml-2">{{ userAddress }}</span></p>
      <p class="text-black">
        QKC Balance:
        <span class="font-mono text-gray-500 ml-2">{{ ethBalance }}</span>
        <span class="ml-2 cursor-pointer text-blue-500 tooltip"
              data-tooltip="The QKC balance is transferable">
          <i class="fas fa-question-circle"></i>
        </span>
      </p>
      <p class="text-black">
        Soul Gas Token Balance:
        <span class="font-mono text-gray-500 ml-2">{{ soulBalance }}</span>
        <span class="ml-2 cursor-pointer text-blue-500 tooltip"
              data-tooltip="The SGT balance is non-transferable and exclusively used for gas fees">
          <i class="fas fa-question-circle"></i>
        </span>
      </p>
      <p class="text-black">
        Total Balance:
        <span class="font-mono text-gray-500 ml-2">{{ totalBalance }}</span>
        <span class="ml-2 cursor-pointer text-blue-500 tooltip"
              data-tooltip="The total balance is the sum of the QKC balance and the SGT balance">
          <i class="fas fa-question-circle"></i>
        </span>
      </p>
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

<style>
.tooltip {
  position: relative;
}

.tooltip::after {
  content: attr(data-tooltip);
  position: absolute;
  bottom: 120%;
  left: 50%;
  transform: translateX(-50%);
  background-color: black;
  color: white;
  padding: 5px 10px;
  border-radius: 4px;
  font-size: 12px;
  visibility: hidden;
  opacity: 0;
  transition: opacity 0.3s ease-out, visibility 0s ease 0.3s;
  max-width: 350px;
  min-width: 230px;
  white-space: normal;
  overflow-wrap: anywhere;
  word-break: break-word;
  text-align: left;
  line-height: 1.5;
}

.tooltip:hover::after {
  visibility: visible;
  opacity: 1;
  transition: opacity 0.3s ease-in;
}
</style>
