<template>
  <medium-editor
    class="content-editable"
    :text="value"
    :options="options"
    @edit="updateHTML"
  />
</template>

<script>
import editor from "vue2-medium-editor";
export default {
  name: "ContentEditable",
  props: {
    value: String
  },
  components: { "medium-editor": editor },
  data() {
    return {
      options: {
        toolbar: { buttons: ["bold", "italic", "underline"] }
      }
    };
  },
  methods: {
    updateHTML: function(operation) {
      this.$emit("input", operation.api.origElements.innerHTML);
    }
  }
};
</script>

<style scoped>
.content-editable {
  height: 100%;
  padding: 24px;
}
</style>
