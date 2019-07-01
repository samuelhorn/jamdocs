<template>
  <Layout :sidebar="false">
    <h1>Jamdocs - the ultimate staic generated documentation theme for the JAM-stack</h1>

    <nav>
      <article>
        <h2><g-link to="/getting-started">Getting started</g-link></h2>
      </article>
      <article>
        <h2><g-link to="/theme-configuration">Theme configuration</g-link></h2>
      </article>
      <article>
        <h2><g-link to="/theme-configuration">Examples</g-link></h2>
      </article>
    </nav>

  </Layout>
</template>

<script>
export default {
  metaInfo: {
    title: 'The ultimate staic generated documentation theme for the JAM-stack'
  }
}
</script>

<style lang="scss" scoped>
h1 {
  text-align: center;
}

nav {
  display: flex;
  justify-content: space-between;
  flex-direction: column;

  @include respond-above(sm) {
    flex-direction: row;
  }

  > * {
    flex: 0 0 30%;
    border: 1px solid shade($sidebarBright, 10%);
    background: $sidebarBright;
    padding: 2rem;
    border-radius: 3px;
    transition: background .15s ease-in-out, border-color .15s ease-in-out;

    .dark & {
      border: 1px solid shade($sidebarDark, 10%);
      background: $sidebarDark;
    }
  }

  a {
    color: inherit;
    text-decoration: none;
  }
}
</style>
