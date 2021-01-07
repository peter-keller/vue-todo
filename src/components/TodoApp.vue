<template>
  <div class="todo-app">
    <div class="todo-app__tasks">
      <todo-task
        class="task"
        v-for="(task, index) in tasks"
        :key="task.date"
        :task="task"
        :canBeRemoved="canDeleteTasks"
        :index="index"
        @input="handleInput"
        @remove="handleRemove"
        @add="handleAdd"
      />
    </div>
    <div class="todo-app__summary">
      <code>
        {{ availableTasks }}
      </code>
    </div>
  </div>
</template>

<script>

import TodoTask from './TodoTask'
export default {
  name: "TodoApp",

  components: {
    TodoTask
  },

  props: {
    tasks: {
      type: Array,
      required: true
    }
  },

  computed: {
    availableTasks () {
      const tasks = this.tasks.map(({ value }) => value)
      return { data: tasks }
    },

    canDeleteTasks () {
      return this.availableTasks.data.length > 1
    }
  },

  methods: {
    handleInput (value) {
      this.$emit('input', value)
    },

    handleRemove (task) {
      this.$emit('remove', task)
    },

    handleAdd (index) {
      this.$emit('add', index)
    }
  }
};
</script>

<style scoped>
.todo-app {
  display: flex;
  justify-content: space-evenly;
}

.todo-app__tasks {
  width: 45vw;
}

.todo-app__summary {
  width: 45vw;
  margin-top: 24px;
  height: fit-content;
  background: var(--preview-bg-color);
  color: var(--preview-text-color);
  padding: 24px;
}

.task {
  margin: 24px 0;
}

code {
  white-space: pre-wrap   
}
</style>
