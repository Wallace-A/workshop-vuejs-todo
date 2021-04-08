<template>
  <div class="task-card new-task"
      @keyup.enter="submitTask(newTitle, newDescription), resetForm()">
    <div>
      <input
        type="text"
        placeholder="What would you like to do?"
        v-model="newTitle"
      />
      <textarea
        placeholder="Add some details about your task..."
        v-model="newDescription"
      ></textarea>
    </div>
  </div>
</template>

<script>
export default {

  data() {
    return {
      newTitle: "",
      newDescription: "",
    };
  },

  methods: {
    submitTask(title, description) {
      this.$emit("add-task", title, description);
    },
    resetForm() {
      this.newTitle = "";
      this.newDescription = "";
    },
  },
}
</script>

<style lang="scss">
@keyframes expand-vertical { from { min-height: 0; height: 0; } to { min-height: 6rem; } }
.task-card.new-task {
  animation: expand-vertical 0.2s;
  overflow: hidden;
  background-color: white;
  border-left: solid 5px #35495e;
  &, &:hover { transform: scale(1.1); box-shadow: 2px 3px 10px rgba(black, 0.2); }
  & + .tasks-list { pointer-events: none; }
  input { font-size: 1.17rem; font-weight: bold; width: 100%; }
  textarea { width: 100%; font-size: 0.9rem; resize: none; }
}
</style>