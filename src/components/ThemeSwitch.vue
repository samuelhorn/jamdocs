<template>
  <button id="themeSwitch" @click="toggleTheme()" aria-label="Switch theme between light and dark">
    <transition name="theme">
      <svg v-if="theme == 'bright'" class="moon" xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24"><path fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21,12.79 C20.5623508,17.5258084 16.5155205,21.1036351 11.7617765,20.9575683 C7.00803241,20.8115015 3.18849849,16.9919676 3.04243171,12.2382235 C2.89636494,7.48447948 6.4741916,3.43764922 11.21,3 C9.15036193,5.78645171 9.43925659,9.66045319 11.8894017,12.1105983 C14.3395468,14.5607434 18.2135483,14.8496381 21,12.79 L21,12.79 Z"/></svg>
    </transition>
    <transition name="theme">
      <svg v-if="theme == 'dark'" class="sun" xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24"><g fill="none" fill-rule="evenodd" stroke-linecap="round" stroke-linejoin="round"><circle cx="12" cy="12" r="5" stroke="currentColor" stroke-width="2"/><path stroke="currentColor" stroke-width="2" d="M12 1L12 3M12 21L12 23M4.22 4.22L5.64 5.64M18.36 18.36L19.78 19.78M1 12L3 12M21 12L23 12M4.22 19.78L5.64 18.36M18.36 5.64L19.78 4.22"/></g></svg>
    </transition>
  </button>
</template>

<script>
export default {
  data() {
    return {
      theme: ''
    }
  },
  methods: {
    setTheme: function() {
      let self = this
      const body = document.querySelector('body')
      const themeSwitch = document.querySelector('#themeSwitch')

      if (process.isClient && localStorage.getItem('theme') === null) {
        localStorage.setItem('theme', 'bright')
        self.theme = 'bright'
      } 
      if (process.isClient) {
        body.classList.add(localStorage.getItem('theme'))
        self.theme = localStorage.getItem('theme')
      }
    },
    toggleTheme: function() {
      let self = this
      const body = document.querySelector('body')

      if (process.isClient) {
        if (body.classList.contains('dark')) {
          localStorage.setItem('theme', 'bright');
          body.classList.remove('dark')
          body.classList.add('bright')
          self.theme = 'bright'
        } else {
          localStorage.setItem('theme', 'dark');
          body.classList.remove('bright')
          body.classList.add('dark')
          self.theme = 'dark'
        }
      }
    }
  },
  mounted () {
    this.setTheme()
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

  &:focus {
    outline: none;
  }

  .dark & {
    color: $textDark;
  }

  .bright & {
    color: $textBright;
  }
}

svg {
  position: absolute;
  top: 12px;
  left: 12px;
}

.theme-enter-active, .theme-leave-active {
  transition: transform .25s ease-in-out, opacity .25s ease-in-out;
}
.theme-enter, .theme-leave-to /* .fade-leave-active below version 2.1.8 */ {
  transform: translateY(20px) scale(.5);
  opacity: 0;
}
</style>


