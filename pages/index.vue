<template>
  <Main>
    <div class="container">
      <div>
        <Logo />
      </div>
    </div>
    <div class="todo-list-wrapper">
      <todo-list />
    </div>
  </Main>
</template>

<script>
import { Vue, Component } from 'vue-property-decorator'

// @ts-ignore
import Logo from '../components/Logo.vue'

// @ts-ignore
import Main from '../components/Main.vue'

import TodoList from '../components/todo-list/Index.vue'

@Component({
  components: {
    Logo,
    Main,
    'todo-list': TodoList
  }
})
class Index extends Vue {
  test = 'hello'

  get calcResult() {
    return 1 + 1
  }
}

export default Index
</script>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
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

.todo-list-wrapper {
  max-width: 1000px;
  padding: 0 8px;
}
</style>
