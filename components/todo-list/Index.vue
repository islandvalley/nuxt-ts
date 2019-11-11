<template>
  <div>
    <h3>Todo List</h3>
    <ul class="todo-list">
      <li v-for="(todoItem, key) in todoList" :key="key" class="todo-item">
        <div>
          {{ todoItem.name }}
        </div>
        <button type="button" @click="updateTodo(todoItem.id)">
          更新する
        </button>
        <button type="button" @click="removeTodo(todoItem.id)">
          削除する
        </button>
      </li>
    </ul>
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
import { Vue, Component } from 'vue-property-decorator'

const getNextKey = (todoList: any) => {
  const keys: number[] = Object.keys(todoList).map((key: string) =>
    parseInt(key)
  )
  const nextKey: number = Math.max(...keys) + 1

  return nextKey
}

@Component
class TodoList extends Vue {
  todoList: any = {
    1: { id: 1, name: '洗濯する' },
    2: { id: 2, name: '掃除する' },
    3: { id: 3, name: '料理する' }
  }
  todoInput: string = ''

  mounted() {
    console.log('mounted!')
  }

  addTodo(): void {
    const nextKey: number = getNextKey(this.todoList)
    this.todoList[nextKey] = {
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

    this.$delete(this.todoList, id)
    this.todoList[id] = {
      id,
      name: newTodo
    }

    window.alert('更新されました')
  }

  // Todoの削除
  removeTodo(id: number) {
    if (
      window.confirm(`"${this.todoList[id].name}"を削除してよろしいですか？`)
    ) {
      this.$delete(this.todoList, id)
      window.alert('削除されました')
    }
  }
}

export default TodoList
</script>

<style scoped>
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
</style>
