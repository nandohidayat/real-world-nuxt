<template>
  <v-app dark>
    <v-layout column justify-center align-center>
      <v-flex xs12 sm8 md6 class="text-center">
        <h1 v-if="error.statusCode === 404">
          {{ pageNotFound }}
        </h1>
        <h1 v-else>
          {{ error.message }}
        </h1>
        <NuxtLink to="/">
          Home page
        </NuxtLink>
      </v-flex>
    </v-layout>
  </v-app>
</template>

<script>
export default {
  layout: 'empty',
  props: {
    error: {
      type: Object,
      default: null
    }
  },
  head() {
    const title =
      this.error.statusCode === 404 ? this.pageNotFound : this.error.message
    return {
      title
    }
  },
  data() {
    return {
      pageNotFound: '404 Not Found'
    }
  }
}
</script>

<style scoped>
h1 {
  font-size: 20px;
}
</style>
