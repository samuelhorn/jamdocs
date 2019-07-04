<template>
  <Layout :sidebar="false">
    <h1>Jamdocs - the ultimate staic generated documentation theme for the JAM-stack</h1>

    <nav>
      <article>
        <h2>
          <g-link to="/getting-started">
            <play-icon />
            Introduction
          </g-link>
        </h2>
      </article>
      <article>
        <h2>
          <g-link to="/theme-configuration">
            <sliders-icon />
            Configuration
          </g-link>
        </h2>
      </article>
      <article>
        <h2>
          <g-link to="/theme-configuration#changing-colors">
            <eye-icon />
            Change colors
          </g-link>
        </h2>
      </article>
    </nav>
  </Layout>
</template>

<script>
// Define icons you need
import { PlayIcon, SlidersIcon, EyeIcon } from 'vue-feather-icons'

export default {
  // Make icons avaliable
  components: {
    PlayIcon,
    SlidersIcon,
    EyeIcon
  },
  metaInfo: {
    title: 'The ultimate staic generated documentation theme for the JAM-stack',
    meta: [
      { key: 'description', name: 'description', content: 'A theme for static site documentation based on Gridsome, ready to deploy to Netlify in one click.' }
    ]
  }
}
</script>

<style lang="scss" scoped>
h1 {
  text-align: center;
  max-width: 600px;
  margin: 1.5em auto 1.5em;

  @include respond-above(md) {
    max-width: 1000px;
  }
}

h2 {
  font-size: 1.4rem;
  margin: 0;
}

nav {
  display: flex;
  justify-content: space-between;
  flex-direction: column;

  @include respond-above(sm) {
    flex-direction: row;
  }

  > * {
    flex: 1 0;
    border: 1px solid shade($sidebarBright, 10%);
    margin: 0 0 1em;
    background: $sidebarBright;
    padding: 2rem;
    border-radius: 3px;
    transition: background .15s ease-in-out, border-color .15s ease-in-out;

    @include respond-above(sm) {
      margin: 0 1em 0;
    }

    .dark & {
      border: 1px solid shade($sidebarDark, 10%);
      background: $sidebarDark;
    }
  }

  a {
    color: inherit;
    text-decoration: none;
    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: column;
  }
}

svg {
  width: 2em;
  height: 2em;
  margin-bottom: 1em;

  @include respond-above(md) {
    width: 3em;
    height: 3em;
  }
}
</style>
