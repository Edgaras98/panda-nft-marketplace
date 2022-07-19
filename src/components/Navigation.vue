<template>
  <header class="sticky-top">
    <nav v-if="!mobile" class="container-lg d-flex justify-content-between align-content-center ">
      <div class="panda-logo d-flex justify-content-center align-items-center">
        <img src="../assets/panda-logo.svg">
        <span>Panda NFT</span>
      </div>
      <div class="header-links d-flex justify-content-center align-items-center text-center">
        <span>Home</span>
        <span>Discover</span>
        <span>Artists</span>
      </div>
      <button class="connect-button" @click="connectToMetamask">
        <span v-if="!userWallet">Connect wallet</span>
        <span v-else>{{ truncatedWalletAddress }}</span>
      </button>
    </nav>
    <nav class="container" v-else>
      <div class="d-flex justify-content-between">
        <div class="panda-logo d-flex justify-content-center align-items-center">
          <img src="../assets/panda-logo.svg">
        </div>
        <a type="button" data-bs-toggle="offcanvas" data-bs-target="#offcanvasScrolling"
           aria-controls="offcanvasScrolling">
          <i class="bi bi-list" style="font-size: 50px; cursor: pointer;"/>
        </a>
      </div>
      <div class="offcanvas offcanvas-start" data-bs-scroll="true" data-bs-backdrop="false"
           tabindex="-1" id="offcanvasScrolling" aria-labelledby="offcanvasScrollingLabel">
        <div class="offcanvas-header">
          <h5 class="offcanvas-title" id="offcanvasScrollingLabel">Navigation</h5>
          <a style="cursor: pointer; font-size: 32px" data-bs-dismiss="offcanvas">
            <i class="bi bi-x-lg"/>
          </a>
        </div>
        <div class="offcanvas-body">
          <p>Try scrolling the rest of the page to see this option in action.</p>
        </div>
      </div>
    </nav>
  </header>
</template>

<script>
export default {
  name: 'Navigation',
  data() {
    return {
      mobile: null,
      windowWidth: null,
      mediumScreenSizePx: 768,
      message: 'Please sign me in!',
      userWallet: sessionStorage.getItem('WalletAddress')
    };
  },
  created() {
    window.addEventListener('resize', this.checkScreenWidth);
    this.checkScreenWidth();
  },
  computed: {
    truncatedWalletAddress(){
      return this.userWallet.slice(0, 6) + '...' + this.userWallet.slice(37, 41)
    },
  },
  methods: {
    checkScreenWidth() {
      this.windowWidth = window.innerWidth;
      this.windowWidth <= this.mediumScreenSizePx ? this.mobile = true : this.mobile = false
    },
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
@import 'src/scss/_header.scss';
</style>
