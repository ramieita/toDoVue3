<template>
  <div class="hello">
    <h2>vue je 3</h2>
    <form @submit.prevent="addNewTask">
      <label> add your new To do </label>
      <input v-model="newTask" name="newTodo" />
      <br />
      <button>add new One</button>
    </form>
    <button @click="markall"> mark all as done </button>
     <button @click="removeall"> remove all   </button>
    <ul>
      <li v-for="(task, index) in tasks" v-bind:key="task.id" class="tasks">
        <h2 :class="{ done: task.done }" @click="markasDone(task)">
          {{ task.content }}
        </h2>
        <button @click="removeTask(index)">remove Todo</button>
      </li>
    </ul>
  </div>
</template>

<script>
import { ref } from "vue";

export default {
  setup() {
    const tasks = ref([]);
    const newTask = ref("");
    function removeTask(index) {
      tasks.value.splice(index);
    }
    function markasDone(task) {
      task.done = !task.done;
    }
    function removeall () {
      tasks.value.length = 0;
    }

    function markall ( ) {
        tasks.value.forEach((task) => task.done= true ); 
    }
    function addNewTask() {
      tasks.value.push({
        id: Date.now(),
        done: false,
        content: newTask.value,
      });
      newTask.value = "";
    }
    return {
      markasDone,
      markall,
      removeTask,
      tasks,
      removeall,
      newTask,
      addNewTask,
    };
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.done {
  text-decoration: line-through;
}
.tasks {
  cursor: pointer;
}
</style>
