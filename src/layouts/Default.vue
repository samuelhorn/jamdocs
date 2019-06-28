<template>
  <div>
    <Header />
    <Sidebar />
    <main class="main">
      <slot/>
    </main>
  </div>
</template>

<static-query>
query {
  metaData {
    siteName
  }
}
</static-query>

<script>
import Header from '~/components/Header.vue'
import Sidebar from '~/components/Sidebar.vue'
import WebFontLoader from 'webfontloader'

export default {
  components: {
    Header,
    Sidebar
  },
  mounted() {
    this.$store.commit('closeSidebar')
    if (process.isClient) {
      if('serviceWorker' in navigator) {
        navigator.serviceWorker
          .register('/sw.js')
          .then(function() { console.log("Service Worker Registered"); });
      }
    }
  },
  created() {
    WebFontLoader.load({
      google: {
        families: ['Source+Sans+Pro:400,400i,700&display=swap']
      }
    });
  }
}
</script>

<style lang="scss" scoped>
.main {
  padding: 140px 30px 30px 30px;
  max-width: 1200px;
  transition: padding .15s ease-in-out;

  @include respond-above(sm) {
    padding: 100px 30px 30px;
    transform: translateX(300px);
    width: calc(100% - 300px);
  }

  @include respond-above(md) {
    padding: 100px 80px 30px;
  }
}
</style>
