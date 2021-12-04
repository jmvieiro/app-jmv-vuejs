<template>
  <v-card :loading="loading" class="mx-auto my-3">
    <v-card-title>{{ ("Tarea #" + task.id) | capitalize }}</v-card-title>
    <v-divider class="mx-4"></v-divider>

    <v-card-text>
      <h3 class="mb-2">{{ task.title | capitalize }}</h3>
      <h4>{{ task.description }}</h4>
    </v-card-text>

    <v-card-text class="py-0">
      <v-chip v-if="task.priority" dark color="red lighten-2"
        >Prioridad: Alta</v-chip
      >
      <v-chip v-else color="success lighten-2">Prioridad: Baja</v-chip>
    </v-card-text>

    <v-divider class="mx-4 my-4"></v-divider>

    <v-card-actions class="mx-2">
      <v-btn
        v-if="!task.done"
        dark
        color="red lighten-1 mb-2"
        @click="deleteTask(task.id)"
      >
        Eliminar
      </v-btn>
      <v-btn
        v-if="!task.done"
        dark
        color="success lighten-1 mb-2"
        @click="markAsDone(task.id)"
      >
        Finalizar
      </v-btn>
      <v-btn
        v-else
        dark
        color="primary lighten-1 mb-2"
        @click="markAsUndone(task.id)"
      >
        Sin finalizar
      </v-btn>
    </v-card-actions>
  </v-card>
</template>

<script>
export default {
  name: "CardTask",
  data: () => ({
    loading: false,
  }),
  props: {
    task: {
      type: Object,
      default: () => {},
    },
    index: {
      type: Number,
      default: 0,
    },
  },
  methods: {
    deleteTask(id) {
      this.loading = true;
      setTimeout(() => {
        this.loading = false;
        this.$emit("deleteTask", id);
      }, 1000);
    },
    markAsDone(id) {
      this.loading = true;
      setTimeout(() => {
        this.loading = false;
        this.$emit("markAsDone", id);
      }, 1000);
    },
    markAsUndone(id) {
      this.loading = true;
      setTimeout(() => {
        this.loading = false;
        this.$emit("markAsUndone", id);
      }, 1000);
    },
  },
};
</script>