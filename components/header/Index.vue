<template>
  <header class="header">
    <Logo />
    <Menu />
  </header>
</template>

<script lang="ts">
import { Vue, Component } from 'vue-property-decorator'
// @ts-ignore
import Logo from './Logo.vue'
// @ts-ignore
import Menu from './Menu.vue'

@Component({
  components: {
    Logo,
    Menu
  }
})
class Index extends Vue {}

export default Index
</script>

<style scoped>
.header {
  background-color: #41b883;
  display: flex;
  justify-content: space-between;
  padding: 20px 8px;
}
</style>
