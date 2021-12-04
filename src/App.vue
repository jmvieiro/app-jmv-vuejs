<template>
  <v-app>
    <v-main>
      <Navbar @showItem="showItem($event)" />
      <v-container v-if="this.show === 1" class="mt-4">
        <h2>Desafío 1: Contador</h2>
      </v-container>
      <v-container v-if="this.show === 2" class="mt-4">
        <h2>Desafío 2: App tareas</h2>
      </v-container>
      <v-container v-else-if="this.show === 3" class="mt-4">
        <h2>Desafío 3: App tareas Cli</h2>
        <v-row>
          <v-col cols="12" xs="12" md="4">
            <FormTasks @saveTask="saveTask($event)" />
          </v-col>
          <v-col xs="12" md="8">
            <ListTasks
              :tasks="tasks"
              @deleteTask="deleteTask($event)"
              @markAsDone="markAsDone($event)"
              @markAsUndone="markAsUndone($event)"
            />
          </v-col>
        </v-row>
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
import Vue from "vue";
import Navbar from "./components/Navbar";
import FormTasks from "./components/FormTasks";
import ListTasks from "./components/ListTasks";

Vue.filter("capitalize", (value) => {
  if (!value) return "";
  return value.toUpperCase();
});

export default {
  name: "App",
  components: {
    Navbar,
    FormTasks,
    ListTasks,
  },
  data: () => ({
    tasks: [],
    show: 3,
  }),
  methods: {
    showItem(item) {
      this.show = item;
    },
    saveTask(data) {
      const newTask = {
        id: Date.now(),
        title: data.title,
        description: data.description,
        priority: data.priority,
        done: false,
      };
      this.tasks.push(newTask);
    },
    deleteTask(id) {
      let aux = this.tasks.filter(function (obj) {
        return obj.id !== id;
      });
      this.tasks = aux;
    },
    markAsDone(id) {
      let aux = [...this.tasks];
      for (var i in aux) {
        aux[i].done = aux[i].id === id ? true : aux[i].done;
      }
      this.tasks = aux;
    },
    markAsUndone(id) {
      let aux = [...this.tasks];
      for (var i in aux) {
        aux[i].done = aux[i].id === id ? false : aux[i].done;
      }
      this.tasks = aux;
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
