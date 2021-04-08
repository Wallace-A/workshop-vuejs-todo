<template>
  <div id="tasks">
    <button class="btn round-icon" @click="newFormVisible = !newFormVisible">
      {{ newFormVisible ? "✕" : "＋" }}
    </button>

    <div
      v-if="newFormVisible"
      class="task-card new-task"
      @keyup.enter="addTask(newTitle, newDescription), resetForm()"
    >
      <NewTask @add-task="addTask" />
    </div>

    <div v-if="tasks.length > 0">
      <TaskCard
        v-for="(task, index) in tasks"
        :key="index"
        :title="task.title"
        :description="task.description"
        :done="task.done">
      </TaskCard>
    </div>

    <p v-else-if="!newFormVisible">You don't have any tasks yet...</p>
  </div>
</template>


<script>
import TaskCard from "./TaskCard"
import NewTask from "./NewTask";
export default {
  components: { TaskCard, NewTask },

  methods: {
    addTask(title, description, done = false) {
      this.tasks.unshift({ title, description, done });
      this.newFormVisible = false;
    },
    resetForm() {
      this.newTitle = ""
      this.newDescription = ""
    },
    toggleTask(taskIndex) {
      const taskToUpdate = this.tasks[taskIndex];
      taskToUpdate.done = !taskToUpdate.done;
      this.$set(this.tasks, taskIndex, taskToUpdate);
    },
  },

  //DATA IS BASICALLY VARIABLES
  data() {
    return {
      tasks: JSON.parse(localStorage.getItem("tasks")) || 
      [],
      newTitle: '',
      newDescription: '',
      newFormVisible: false,
    };
  },
  //SAVE TO LOCAL STORAGE
  watch: {
    tasks() {
      localStorage.setItem("tasks", JSON.stringify(this.tasks));
    },
  },
};
</script>

<style lang="scss">
</style>