<template>
  <nuxt-content :document="page" />
</template>

<script>
export default {
  async asyncData({ $content, params, error }) {
    const slug = params.slug || "index"
    const page = await $content(slug)
      .fetch()
      .catch((err) => {
        error({
          statusCode: 404,
          message: "Page not found. Error: " + err.message,
        })
      })

    return { page }
  },

  head() {
    return {
      title: this.page.title,
    }
  },
}
</script>

<style></style>
