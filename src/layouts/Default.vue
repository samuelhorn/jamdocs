<template>
  <div>
    <Header :scroll="pageScrolled" />
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
  data() {
    return {
      pageScrolled: false
    }
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
    },
    handleScroll: function() {
      let mainNavLinks = document.querySelectorAll('.topic.active + ul .sub-topic')
      let fromTop = window.scrollY

      if ((fromTop > 0 && this.pageScrolled == false) || (fromTop == 0 && this.pageScrolled == true)) {
        this.pageScrolled = !this.pageScrolled
      }

      mainNavLinks.forEach(link => {
        let section = document.querySelector(link.hash)
        let allCurrent = document.querySelectorAll('.current'), i

        if (section.offsetTop <= fromTop) {
          for (i = 0; i < allCurrent.length; ++i) {
            allCurrent[i].classList.remove('current')
          }
          link.classList.add('current')
        } else {
          link.classList.remove('current')
        }
      })
    }
  },
  beforeMount () {
    this.stateFromSize()
  },
  mounted() {
    window.addEventListener('scroll', throttle(this.handleScroll, 50))
    //window.addEventListener('resize', throttle(this.stateFromSize, 200))
  },
  beforeUpdate () {
    window.removeEventListener('scroll', throttle(this.handleScroll, 50))
  },
  updated () {
    window.addEventListener('scroll', throttle(this.handleScroll, 50))
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
