<template>
  <div>
    <v-tabs v-model="tab" align-with-title>
      <v-tabs-slider color="yellow"></v-tabs-slider>
      <v-tab v-for="item in items" :key="item">
        {{ item }}
      </v-tab>
    </v-tabs>
    <v-tabs-items v-model="tab">
      <v-tab-item v-for="item in items" :key="item">
        <v-card flat>
          <v-card-text v-if="item.toLowerCase() === 'tareas pendientes'">
            <ListTasksDetail
              :tasks="tasks.filter((t) => !t.done)"
              :done="false"
              @deleteTask="deleteTask($event)"
              @markAsDone="markAsDone($event)"
              @markAsUndone="markAsUndone($event)"
            />
          </v-card-text>
          <v-card-text v-else>
            <ListTasksDetail
              :tasks="tasks.filter((t) => t.done)"
              :done="true"
              @deleteTask="deleteTask($event)"
              @markAsDone="markAsDone($event)"
              @markAsUndone="markAsUndone($event)"
            />
          </v-card-text>
        </v-card>
      </v-tab-item>
    </v-tabs-items>
  </div>
</template>

<script>
import ListTasksDetail from "./ListTasksDetail";

export default {
  name: "ListTasks",
  components: {
    ListTasksDetail,
  },
  data() {
    return {
      tab: null,
      items: ["Tareas pendientes", "Tareas finalizadas"],
    };
  },
  props: {
    tasks: {
      type: Array,
      default: () => [],
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