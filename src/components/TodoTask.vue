<template>
  <div class="todo-task">
    <div class="todo-task__content">
      <ContentEditable
        v-model="task.value"
      />
    </div>
    <div class="todo-task__actions">
      <PdButton
        display-style="standard"
        @click="handleAdd"
      >
        +
      </PdButton>
      <PdButton
        display-style="alert"
        :disabled="!canBeRemoved"
        @click="handleRemove"
      >
        -
      </PdButton>
    </div>
  </div>
</template>

<script>
import PdButton from './PdButton'
import ContentEditable from './ContentEditable'

export default {
  name: 'TodoTask',

  components: {
    PdButton,
    ContentEditable
  },

  props: {
    task: {
      type: Object,
      required: true
    },

    canBeRemoved: {
      type: Boolean,
      default: false
    },

    index: {
      type: Number,
      required: true
    }
  },

  methods: {
    handleRemove () {
      this.$emit('remove', this.task)
    },

    handleAdd () {
      this.$emit('add', this.index)
    }
  }
}
</script>

<style scoped>
.todo-task {
  width: 100%;
  display: flex;
  justify-content: space-between;
  min-height: 96px;
}

.todo-task__content {
  width: 100%;
  min-height: 100%;
  background-color: var(--content-editable-bg-color);
}

.todo-task__actions {
  display: flex;
}

.todo-task__input {
  width: 100%;
  height: 100%;
}
</style>
