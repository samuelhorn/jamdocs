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
import throttle from 'lodash/throttle'

export default {
  components: {
    Header,
    Sidebar
  },
  watch: {
    '$route' () {
      this.$store.commit('closeSidebar')
    }
  },
  methods: {
    stateFromSize: function() {
      if (window.getComputedStyle(document.body, ':before').content == '"small"') {
        this.$store.commit('closeSidebar')
      } else {
        this.$store.commit('openSidebar')
      }
    }
  },
  beforeMount () {
    this.stateFromSize()
  },
  mounted() {
    //window.addEventListener('resize', throttle(this.stateFromSize, 200))
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
