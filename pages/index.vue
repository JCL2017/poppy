<template>
  <div class="container">
    <IndexCarousel />
    <IndexBanner />
    <IndexInformation />
    <IndexModule />
  </div>
</template>

<script>
import IndexCarousel from '~/components/IndexCarousel.vue'
import IndexBanner from '~/components/IndexBanner.vue'
import IndexInformation from '~/components/IndexInformation.vue'
import IndexModule from '~/components/IndexModule.vue'

export default {
  components: {
    IndexCarousel,
    IndexBanner,
    IndexInformation,
    IndexModule
  }
}
</script>

<style scoped>
.container {
  margin: 0 auto;
  min-height: 100vh;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family: 'Quicksand', 'Source Sans Pro', -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>
