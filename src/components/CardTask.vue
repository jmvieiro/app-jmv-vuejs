<template>
  <v-card class="mx-auto my-12">
    <v-card-title>Tarea #{{ task.id }}</v-card-title>

    <v-card-text>
      <h2 class="mb-2">{{ task.title }}</h2>
      <h4>{{ task.description }}</h4>
    </v-card-text>

    <v-card-text class="py-0">
      <v-alert v-if="task.priority" color="red lighten-2 mb-0" dark>
        Prioridad: Alta
      </v-alert>
      <v-alert v-else color="success lighten-2" dark> Prioridad: Baja </v-alert>
    </v-card-text>

    <v-divider class="mx-4 my-4"></v-divider>

    <v-card-actions class="mx-2">
      <v-btn dark color="red lighten-1 mb-2" @click="deleteTask(index)">
        Eliminar
      </v-btn>
    </v-card-actions>
  </v-card>
</template>

<script>
export default {
  name: "CardTask",
  props: {
    task: {
      type: Object,
      default: () => {},
    },
    index: {
      type: Number,
      default: 0,
    },
    deleteTask: {
      type: Function,
      default: () => {},
    },
  },
};
</script>