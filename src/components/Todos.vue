<template>
  <div class="todo-app" id="app">
    <div class="todo-app-presentation">
      <h1 class="todo-app-title">Todo App</h1>
      <h4 class="todo-app-text">List the things you are willing to do...</h4>
    </div>

    <div class="todo-container">
      <form @submit.prevent="addTodo(todo)">
        <div class="input-group">
          <input type="text" v-model="todo.text" class="form-input" placeholder="New todo" />
          <button class="btn btn-primary input-group-btn">Add</button>
        </div>
      </form>

      <div class="todo-list" v-for="t in todos" :key="t.id">
        <div class="tile" :class="{ checked: t.checked }">
          <div class="tile-icon">
            <i class="icon icon-time centered"></i>
          </div>
          <div class="tile-content">
            <div class="tile-subtitle">
              {{ t.text }}
            </div>
          </div>
          <div class="tile-action">
            <input type="checkbox" :checked="t.checked" @change="toggleTodo(todo, t)" />
          </div>
        </div>
      </div>

    </div>
  </div>
</template>

<script>

export default {
  name: 'app',
  data() {
    return {
      todos: [
        { id: 1, text: 'Learn HTML', checked: true },
        { id: 2, text: 'Learn CSS', checked: true },
        { id: 3, text: 'Learn Javascript', checked: true },
        { id: 4, text: 'Learn Node', checked: true },
        { id: 5, text: 'Learn Vue', checked: true },
        { id: 6, text: 'Learn Go', checked: false },
        { id: 7, text: 'Learn Rust', checked: false },
        { id: 12, text: 'Be a good father', checked: true },
      ], todo: { checked: false }
    };
  },
  methods: {
    addTodo(todo) {
      todo.id = Date.now();
      this.todos.push(todo);
      this.todo = { checked: false }
    },
    toggleTodo(todo, t) {
      const index = this.todos.findIndex(item => item.id === t.id);

      if (index > -1) {
        const checked = !this.todos[index].checked;
        this.todos[index].checked = checked;
      }
    }
  }
};
</script>

<style scoped>
.todo-app {
  width: 700px;
  margin: 10px auto;
}

.todo-app-presentation {
  margin: 10px 20px;
}

.todo-app-title {
  font-size: 22px;
  color: #333;
}

.todo-app-text {
  font-size: 14px;
  color: #999;
  font-style: italic;
  font-weight: 100;
}

.todo-container {
  background-color: #fafafa;
  min-height: 300px;
  padding: 20px;
  box-shadow: 1px 1px 1px 1px rgba(0, 0, 0, 0.1);
  border-radius: 10px;
}

.todo-title {
  color: rebeccapurple;
}

.todo-list {
  padding: 10px;
}

.checked {
  text-decoration: line-through;
  color: lightgray;
}
</style>