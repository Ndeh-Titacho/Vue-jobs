<script setup>
import HelloWorld from "@/components/HelloWorld.vue";
import TheWelcome from "@/components/TheWelcome.vue";
</script>

<template>
  <h1>Vue Jobs</h1>
  <HelloWorld />
  <TheWelcome />

  <template />
</template>

<template>
  <h1>{{ name }}</h1>
  <br />
  <p v-if="this.status === 'active'">User is active</p>
  <p v-else-if="this.status === 'pending'">User is pending</p>
  <p v-else>User is active</p>
  <br />

  <h3>Task:</h3>
  <ul>
    <li v-for="task in tasks" :key="task">{{ task }}</li>
  </ul>
  <br />
  <button v-on:click="toggleStatus">check status</button>
</template>

<script>
export default {
  setup() {
    const name = "Ndeh Titacho";
    const status = "active";
    const tasks = ["Task 1", "Task 2", "Task 3"];

    const toggleStatus = () => {
      if (this.status === "active") {
        this.status = "pending";
      } else if (this.status === "pending") {
        this.status = "inactive";
      } else {
        this.status = "active";
      }
    };
    return {
      name,
      status,
      tasks,
      toggleStatus,
    };
  },
};
</script>

<script setup>
import { ref, onMounted } from "vue";

const name = ref("Ndeh Titacho");
const status = ref("active");
const tasks = ref(["Task 1", "Task 2", "Task 3"]);
const newTask = ref("");

const toggleStatus = () => {
  if (status.value === "active") {
    status.value = "pending";
  } else if (status.value === "pending") {
    status.value = "inactive";
  } else {
    status.value = "active";
  }
};

const addTask = () => {
  if (newTask.value.trim() !== "") {
    tasks.value.push(newTask.value);
    newTask.value = "";
  }
};

const deleteTask = (index) => {
  tasks.value.splice(index, 1);
};

onMounted(async () => {
  try {
    const response = await fetch("https://jsonplaceholder.typicode.com/todos");
    const data = await response.json();
    tasks.value = data.map((task) => task.title);
  } catch (error) {
    console.log("Error fetching task");
  }
});
</script>

<template>
  <h1>{{ name }}</h1>
  <br />
  <p v-if="status.value === 'active'">User is active</p>
  <p v-else-if="status.value === 'pending'">User is pending</p>
  <p v-else>User is active</p>
  <br />

  <h3>Task:</h3>
  <br />
  <form @submit.prevent="addTask">
    <label for="newtask">NewTask</label>
    <input type="text" name="newtask" id="" v-model="newTask" />
    <button type="submit">Submit</button>
  </form>
  <br />
  <ol>
    <li v-for="(task, index) in tasks" :key="task">
      <span>{{ task }}</span>
      <button @click="deleteTask(index)">X</button>
    </li>
  </ol>
  <br />
  <button @click="toggleStatus">check status</button>
</template>
