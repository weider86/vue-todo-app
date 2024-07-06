<template>
  <div class="todo-app" id="app">
    <div class="todo-app-presentation">
      <h1 class="todo-app-title">Todo App</h1>
      <h4 class="todo-app-description">List the things you are willing to do...</h4>
    </div>
    <div class="todo-container">
      <form @submit.prevent="addTodo(todo)">
        <div class="input-group">
          <input type="text" v-model="todo.description" class="form-input" placeholder="New todo" />
          <button class="btn btn-primary input-group-btn">Add</button>
        </div>
      </form>

      <div class="todo-list">

        <div class="tile" v-for="t in todos" :key="t.id">
          <div class="tile-icon">
            <i class="icon icon-time centered"></i>
          </div>
          <div class="tile-content">
            <div class="tile-subtitle">
              {{ t.description }}
            </div>
          </div>
          <div class="tile-action">
            <button class="btn btn-link">Done</button>
            <button class="btn btn-link">
              <span class="text-error">Remove</span>
            </button>
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
    return { todos: [], todo: { checked: false } };
  },
  methods: {
    addTodo(todo) {
      todo.id = Date.now();
      this.todos.push(todo);
      this.todo = { checked: false }
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

.todo-app-description {
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
  padding: 20px;
}
</style>