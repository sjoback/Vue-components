<template>
    <div v-html="$prismic.asHtml(content)"></div>
</template>
<script>
  export default {
      props: {
          content: {
              type: Array,
              required: true
          }
      }
  }
</script>
