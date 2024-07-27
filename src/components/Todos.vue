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
            <label class="switch">
              <input type="checkbox" :checked="t.checked" @change="toggleTodo(todo, t)" />
              <span class="slider round"></span>
            </label>
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
  padding: 20px 10px 0px 20px;
}

.checked {
  text-decoration: line-through;
  color: lightgray;
}

.btn.btn-primary {
  background-color: #2196F3;
  border-color: #2196F3;
  border-radius: 10px;
}

.form-input {
  border-radius: 10px;
}


/* TODO: Export to new component */
.switch {
  position: relative;
  display: inline-block;
  width: 50px;
  height: 26px;
}

.switch input {
  opacity: 0;
  width: 0;
  height: 0;
}

.slider {
  position: absolute;
  cursor: pointer;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: #ccc;
  -webkit-transition: .4s;
  transition: .4s;
}

.slider:before {
  position: absolute;
  content: "";
  height: 22px;
  width: 22px;
  left: 3px;
  bottom: 2px;
  background-color: white;
  -webkit-transition: .4s;
  transition: .4s;
}

input:checked+.slider {
  background-color: #2196F3;
}

input:focus+.slider {
  box-shadow: 0 0 1px #2196F3;
}

input:checked+.slider:before {
  -webkit-transform: translateX(22px);
  -ms-transform: translateX(22px);
  transform: translateX(22px);
}

/* Rounded sliders */
.slider.round {
  border-radius: 34px;
}

.slider.round:before {
  border-radius: 50%;
}
</style>