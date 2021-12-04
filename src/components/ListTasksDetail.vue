<template>
  <v-row v-if="tasks.length === 0">
    <v-col>
      <div class="mx-auto my-3 text-center d-block">
        <v-alert v-if="done" color="primary lighten-2" dark
          >¡No tenés tareas finalizadas!</v-alert
        >
        <v-alert v-else color="primary lighten-2" dark
          >¡No tenés tareas pendientes!</v-alert
        >
      </div>
    </v-col>
  </v-row>
  <v-row v-else>
    <v-col v-for="(task, i) in tasks" :key="i" cols="12" sm="6">
      <CardTask
        :task="task"
        :index="i"
        @deleteTask="deleteTask($event)"
        @markAsDone="markAsDone($event)"
        @markAsUndone="markAsUndone($event)"
      />
    </v-col>
  </v-row>
</template>

<script>
import CardTask from "./CardTask";

export default {
  name: "ListTasksDetail",
  components: {
    CardTask,
  },
  props: {
    tasks: {
      type: Array,
      default: () => [],
    },
    done: {
      type: Boolean,
      default: false,
    },
  },
  methods: {
    deleteTask(index) {
      this.$emit("deleteTask", index);
    },
    markAsDone(index) {
      this.$emit("markAsDone", index);
    },
    markAsUndone(index) {
      this.$emit("markAsUndone", index);
    },
  },
};
</script>