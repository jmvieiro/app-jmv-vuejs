<template>
  <v-app>
    <v-main>
      <Navbar />
      <v-container class="mt-4">
        <h2>Desafío 3: App tareas Cli</h2>
        <v-row>
          <v-col lg="3">
            <FormTasks :saveTask="saveTask" />
          </v-col>
          <v-col lg="9">
            <ListTasks :tasks="tasks" :deleteTask="deleteTask" />
          </v-col>
        </v-row>
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
import Navbar from "./components/Navbar";
import FormTasks from "./components/FormTasks";
import ListTasks from "./components/ListTasks";

export default {
  name: "App",

  components: {
    Navbar,
    FormTasks,
    ListTasks,
  },

  data: () => ({
    tasks: [],
  }),

  methods: {
    saveTask(title, description, priority) {
      const newTask = {
        id: Date.now(),
        title: title,
        description: description,
        priority: priority,
      };
      this.tasks.push(newTask);
    },
    deleteTask(index) {
      this.tasks.splice(index, 1);
    },
  },
  watch: {
    tasks() {
      localStorage.setItem("tasks", JSON.stringify(this.tasks));
    },
  },
  mounted() {
    const itemsLocalStorage = localStorage.getItem("tasks");
    if (itemsLocalStorage) this.tasks = JSON.parse(itemsLocalStorage);
  },
};
</script>
