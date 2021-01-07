<template>
  <div id="app">
    <TodoApp
      :tasks="tasks"
      @remove="handleRemove"
      @add="handleAdd"
    />
  </div>
</template>

<script>
import users from "./users.json";
import TodoApp from "./components/TodoApp";

export default {
  name: "App",

  components: {
    TodoApp
  },

  data () {
    // Ideally would include current user and only fetch data that
    // belongs to the user, and nothing hardcoded like this
    return {
      tasks: users[0].todos
    }
  },

  methods: {
    handleRemove (taskToRemove) {
      this.tasks = this.tasks.filter(task => task !== taskToRemove)
    },

    handleAdd (index) {
      const newItem = {
        date: new Date().toISOString(),
        type: 'html',
        value: ''
      }

      this.tasks.splice(index + 1, 0, newItem)
    }
  }
};
</script>

<style>
#app {
  color: #000000;
  padding: 10px;
  font-family: monospace;
}
* {
  box-sizing: border-box;
}
:root {
  --bg-color: #dddddd;
  --btn-add-bg-color: #9acd31;
  --btn-delete-bg-color: #ce5c5c;
  --btn-disabled-bg-color: #ccc;
  --preview-bg-color: #000;
  --preview-text-color: #fff;
  --content-editable-bg-color: #f6f5f5;
}
html, body{
  background: var(--bg-color);
}
</style>
