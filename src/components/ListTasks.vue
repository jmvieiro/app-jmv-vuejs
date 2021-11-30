<template>
  <div>
    <v-row v-if="tasks.length === 0">
      <v-col>
        <div class="mx-auto my-12 text-center d-block">
          <v-alert color="success lighten-2" dark
            >¡No tenés tareas pendientes!</v-alert
          >
        </div>
      </v-col>
    </v-row>
    <v-row v-else>
      <v-col v-for="(task, i) in tasks" :key="i" lg="4">
        <CardTask :task="task" :index="i" :deleteTask="deleteTask" />
      </v-col>
    </v-row>
  </div>
</template>

<script>
import CardTask from "./CardTask";

export default {
  name: "ListTasks",
  components: {
    CardTask,
  },
  props: {
    tasks: {
      type: Array,
      default: () => [],
    },
    deleteTask: {
      type: Function,
      default: () => {},
    },
  },
};
</script>