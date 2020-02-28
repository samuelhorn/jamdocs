<template>
  <div class="site">
    <Header :menuToggle="sidebar" />
    <Sidebar v-if="sidebar" />
    <main class="main" :class="{'main--no-sidebar': !sidebar, 'main--sidebar-is-open' : this.$store.state.sidebarOpen}">
      <slot/>
    </main>
  </div>
</template>

<static-query>
query {
  metadata {
    siteName
  }
}
</static-query>

<script>
import Header from '~/components/Header.vue'
import Sidebar from '~/components/Sidebar.vue'

export default {
  components: {
    Header,
    Sidebar
  },
  props: {
    sidebar: {
      type: Boolean,
      default: true
    }
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
  }
}
</script>

<style lang="scss" scoped>
.site {
  overflow: hidden;
}

.main {
  padding: 100px 30px 30px 30px;
  max-width: 800px;
  transition: transform .15s ease-in-out;

  @include respond-above(sm) {
    padding: 100px 30px 30px;
    transform: translateX(300px);
    width: calc(100% - 300px);
  }

  @include respond-above(md) {
    padding: 100px 80px 30px;
  }

  &--no-sidebar {
    transform: translate(0);
    margin: 0 auto;
    width: 100%;
    max-width: 1400px;
  }

  &--sidebar-is-open {
    transform: translate(300px);
  }
}
</style>
