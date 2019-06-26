<template>
  <button @click="toggleMenu()" class="toggle">
    <transition name="toggle">
      <svg v-if="!menuOpen" class="open" xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24">
        <path fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 12L21 12M3 6L21 6M3 18L21 18"/>
      </svg>
    </transition>
    <transition name="toggle">
      <svg v-if="menuOpen" class="close" xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24">
        <path fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M18 6L6 18M6 6L18 18"/>
      </svg>
    </transition>
  </button>
</template>

<script>
import throttle from 'lodash/throttle'

export default {
  data() {
    return {
      menuOpen: false
    }
  },
  methods: {
    toggleMenu: function(event) {
      this.$emit('toggled', 'true')
      this.menuOpen = !this.menuOpen
    },
    pageSize: function() {
      if (window.getComputedStyle(document.body, ':before').content == '"large"') {
        this.menuOpen = true
      } else {
        this.menuOpen = false
      }
    },
  },
  mounted () {
    this.pageSize()
    window.addEventListener('resize', throttle(this.pageSize, 200))
  }
}
</script>

<style lang="scss" scoped>
button {
  background: none;
  border: 0;
  padding: 0;
  transition: color .15s ease-in-out;
  cursor: pointer;
  width: 48px;
  height: 48px;
  position: relative;

  @include respond-above(sm) {
    display: none;
  }

  &:focus {
    outline: none;
  }
  
  .bright & {
    color: $textBright;
  }

  .dark & {
    color: $textDark;
  }
}

svg {
  position: absolute;
  top: 12px;
  left: 12px;
}

.toggle-enter-active, .toggle-leave-active {
  transition: transform .25s ease-in-out, opacity .25s ease-in-out;
}
.toggle-enter, .toggle-leave-to /* .fade-leave-active below version 2.1.8 */ {
  transform: rotateZ(-180deg);
  opacity: 0;
}
</style>

