<template>
  <main>
    <Header />
    <slot />
    <Footer />
  </main>
</template>

<script lang="ts">
import { Vue, Component } from 'vue-property-decorator'

// @ts-ignore
import Header from './header/Index.vue'
// @ts-ignore
import Footer from './Footer.vue'

@Component({
  components: {
    Header,
    Footer
  }
})
class Main extends Vue {}

export default Main
</script>
