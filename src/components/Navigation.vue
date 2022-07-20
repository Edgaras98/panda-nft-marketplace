<template>
  <header id="navigation" class="sticky-top pt-md-3">
    <!-- Desktop navigation-->
    <nav class="container d-none d-md-flex justify-content-md-between align-content-md-center">
      <div class="panda-logo d-flex justify-content-center align-items-center">
        <img src="../assets/panda-logo.svg" alt="brand">
        <span class="brand-title">Panda NFT</span>
      </div>
      <div class="navigation-links d-flex justify-content-center align-items-center text-center">
        <span v-for="(link, index) in links" :key="index" class="link">{{ link.title }}</span>
      </div>
      <connect-button></connect-button>
    </nav>
    <!-- Mobile navigation    -->
    <nav class="container d-block d-md-none">
      <div class="d-flex justify-content-between">
        <div class="panda-logo d-flex justify-content-center align-items-center">
          <img src="../assets/panda-logo.svg" alt="brand">
        </div>
        <a type="button" class="offcanvas-scroll" data-bs-toggle="offcanvas"
           data-bs-target="#offcanvasScrolling"
           aria-controls="offcanvasScrolling">
          <i class="bi bi-list icons"/>
        </a>
      </div>
      <div class="offcanvas offcanvas-start" data-bs-scroll="true" data-bs-backdrop="false"
           tabindex="-1" id="offcanvasScrolling" aria-labelledby="offcanvasScrollingLabel">
        <div class="offcanvas-header">
          <h5 class="offcanvas-title" id="offcanvasScrollingLabel">
            <connect-button></connect-button>
          </h5>
          <a class="off-canvas" data-bs-dismiss="offcanvas">
            <i class="bi bi-x-lg icons"/>
          </a>
        </div>
        <div class="offcanvas-body col-12 mx-auto">
          <div v-for="(link, index) in links" :key="index"
               class="d-flex justify-content-between align-items-center border-top my-2">
            <i class="icon" :class="link.icon"></i>
            <a class="d-block link">
              {{ link.title }}
            </a>
          </div>
        </div>
      </div>
    </nav>
  </header>
</template>

<script>
import ConnectButton from '@/components/ConnectButton';

export default {
  name: 'Navigation',
  components: { ConnectButton },
  data() {
    return {
      links: [
        {
          title: 'Home',
          icon: 'bi bi-house'
        },
        {
          title: 'Discover',
          icon: 'bi bi-search'
        },
        {
          title: 'Artists',
          icon: 'bi bi-people-fill'
        }
      ]
    };
  },
};
</script>
<style lang="scss">
@import '../scss/navigation';
</style>
