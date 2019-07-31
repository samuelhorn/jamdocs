<template>
  <g-link to="/" class="logo" title="Back to home">
    <transition name="theme">
      <div v-if="color == 'dark'">
        <g-image src="~/assets/img/logo-bright.svg" alt="logo" />
      </div>
    </transition>
    <transition name="theme">
      <div v-if="color == 'bright'">
        <g-image src="~/assets/img/logo-dark.svg" alt="logo" />
      </div>
    </transition>
  </g-link>
</template>

<script>
export default {
  props: {
    color: {
      type: String,
      required: true
    }
  }
}
</script>

<style lang="scss" scoped>
.logo {
  height: 40px;
  display: block;
  transition: color .15s ease-in-out;
  color: $textBright;
  position: relative;
  perspective: 200px;

  div {
    height: 40px;
    position: absolute;
    top: 0;
    left: 0;
  }

  img {
    height: 100%;
    width: auto;
  }
}

.theme-enter-active, .theme-leave-active {
  transition: opacity .15s ease-in-out;
}
.theme-enter, .theme-leave-to /* .fade-leave-active below version 2.1.8 */ {
  opacity: 0;
}
</style>


