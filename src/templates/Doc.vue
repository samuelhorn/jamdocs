<template>
  <Layout>
    <h1>
      {{ $page.doc.title }}
    </h1>
     <div v-html="$page.doc.content" />
  </Layout>
</template>

<page-query>
query Doc ($path: String!) {
  doc: doc (path: $path) {
    title
    path
    date (format: "D. MMMM YYYY")
    timeToRead
    description
    content
  }
}
</page-query>

<script>
export default {
}
</script>


<style lang="scss" scoped>
h1 {
  margin-top: 0;
}
</style>

