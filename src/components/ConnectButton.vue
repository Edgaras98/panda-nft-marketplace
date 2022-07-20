<template>
  <button class="btn btn-primary connect-button" @click="connectToMetamask">
    <span v-if="!userWallet">Connect wallet</span>
    <span class="d-flex justify-content-between align-items-center" v-else>
      <span class="d-block mr-4 green-dot"></span>
      <span>{{ truncatedWalletAddress }}</span>
    </span>
  </button>
</template>

<script>
export default {
  name: 'ConnectButton',
  data() {
    return {
      message: 'Please sign me in!',
      userWallet: sessionStorage.getItem('WalletAddress')
    };
  },
  computed: {
    truncatedWalletAddress() {
      return this.userWallet.slice(0, 6) + '...' + this.userWallet.slice(37, 41);
    },
  },
  methods: {
    checkIfMetamaskIsMetamaskEnabled() {
      if (!window.ethereum) {
        return alert('MetaMask not detected. Please try again from a MetaMask enabled browser.');
      }
      this.connectToMetamask();
    },
    async connectToMetamask() {
      const web3 = new Web3(window.ethereum);
      const address = (await web3.eth.requestAccounts())[0];
      await web3.eth.personal.sign(this.message, address);

      if (address) {
        this.userWallet = address;
        sessionStorage.setItem('WalletAddress', address);
      }
    }
  },
};
</script>
<style lang="scss">
@import '../scss/buttons';
</style>

