<template>
  <div class="todo-wrapper">
    <h3>完了したTodo</h3>
    <div>
      <ul v-if="Object.keys(todo.complete).length > 0" class="todo-list">
        <li v-for="(todo, key) in todo.complete" :key="key" class="todo-item">
          <div>
            {{ todo.name }}
          </div>
          <div class="buttons-wrapper">
            <button type="button" @click="cancelComletedTodo(todo)">
              未完了にする
            </button>
          </div>
        </li>
      </ul>
      <div v-else>完了したTodoはありません</div>
    </div>
    <h3>Todo</h3>
    <div>
      <ul v-if="Object.keys(todo.wip).length > 0" class="todo-list">
        <li v-for="(todo, key) in todo.wip" :key="key" class="todo-item">
          <div>
            {{ todo.name }}
          </div>
          <div class="buttons-wrapper">
            <button type="button" @click="completeTodo(todo)">
              完了する
            </button>
            <button type="button" @click="updateTodo(todo.id)">
              更新する
            </button>
            <button type="button" @click="removeTodo(todo.id)">
              削除する
            </button>
          </div>
        </li>
      </ul>
      <div v-else>Todoはありません</div>
    </div>
    <h3>新規登録</h3>
    <input
      v-model="todoInput"
      type="text"
      class="todo-input"
      placeholder="やることを入力"
    />
    <button type="button" @click="addTodo">登録</button>
  </div>
</template>

<script lang="ts">
import { Vue, Component, Prop } from 'vue-property-decorator'
import { Todo } from '../../typings/todo'

const getNextKey = (todoList: any): number => {
  const keys: number[] = Object.keys(todoList).map((key: string) =>
    parseInt(key)
  )

  return Math.max(...keys) + 1
}

@Component
class TodoList extends Vue {
  todo: { [K: string]: Todo[] | any } = {
    complete: {},
    wip: {
      1: { id: 1, name: '洗濯する' },
      2: { id: 2, name: '掃除する' },
      3: { id: 3, name: '料理する' }
    }
  }

  @Prop({ type: String, required: true })
  todoInput: string = ''

  mounted() {
    console.log('mounted!')
  }

  cancelComletedTodo(todo: Todo): void {
    const { id, name } = todo
    this.todo.wip[id] = {
      id,
      name
    }

    this.$delete(this.todo.complete, id)
  }

  completeTodo(todo: Todo): void {
    const { id, name } = todo
    this.todo.complete[id] = {
      id,
      name
    }
    console.log(this.todo.complete)

    this.$delete(this.todo.wip, id)
  }

  addTodo(): void {
    const nextKey: number = getNextKey(this.todo.wip)
    this.todo.wip[nextKey] = {
      id: nextKey,
      name: this.todoInput
    }

    this.todoInput = ''
  }

  // todoの更新
  updateTodo(id: number) {
    const newTodo = window.prompt('変更後のTodoを入力してください', '')

    if (!newTodo) {
      return
    }

    this.$delete(this.todo.wip, id)
    this.todo.wip[id] = {
      id,
      name: newTodo
    }

    window.alert('更新されました')
  }

  // Todoの削除
  removeTodo(id: number) {
    if (
      window.confirm(`"${this.todo.wip[id].name}"を削除してよろしいですか？`)
    ) {
      this.$delete(this.todo.wip, id)
      window.alert('削除されました')
    }
  }
}

export default TodoList
</script>

<style scoped>
.todo-wrapper {
  min-height: calc(100vh - 96px);
  padding: 20px 0;
}

.todo-list {
  padding: 0;
}

.todo-item {
  border: 1px solid #ddd;
  border-radius: 4px;
  display: flex;
  justify-content: space-between;
  margin: 8px 0;
  list-style-type: none;
  padding: 8px;
}

.todo-input {
  border: 1px solid #ddd;
  border-radius: 4px;
  list-style-type: none;
  padding: 8px;
}

.buttons-wrapper {
}
</style>
