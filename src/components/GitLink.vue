<template>
  <a class="link" href="https://github.com/samuelhorn/jamdocs" title="Git-repository" aria-label="This documentation on git">
    <github-icon class="icon" />
    Jamdocs on Github
  </a>
</template>

<script>
import { GithubIcon } from 'vue-feather-icons'

export default {
  components: {
    GithubIcon
  }
}
</script>

<style lang="scss" scoped>
.link {
  display: block;
  padding: 6px 10px;
  border-radius: 3px;
  font-size: 12px;
  line-height: 18px;
  font-weight: 700;
  transition: color .15s ease-in-out, background .15s ease-in-out;

  &:focus {
    outline: none;
  }

  .dark & {
    color: $textBright;
    background: $backgroundBright;
  }

  .bright & {
    color: $textDark;
    background: $backgroundDark;
  }
}

svg {
  width: 18px;
  height: 18px;
  vertical-align: -6px;
  margin-right: 4px;
}
</style>

