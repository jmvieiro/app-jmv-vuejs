<template>
  <div>
    <v-card :loading="loading" class="mx-auto my-12">
      <v-card-title>Agregar tarea</v-card-title>

      <v-card-text>
        <v-text-field
          ref="title"
          label="Título"
          hide-details="auto"
          v-model="inputTitle"
        ></v-text-field>
        <v-text-field
          label="Descripción"
          hide-details="auto"
          v-model="inputDescription"
        ></v-text-field>
        <v-checkbox
          v-model="inputPriority"
          id="inputPriority"
          :label="`Prioritaria`"
        ></v-checkbox>
      </v-card-text>

      <v-divider class="mx-4 my-4"></v-divider>

      <v-card-actions class="mx-2">
        <v-btn color="primary lighten-1 mb-2" @click="readTask">
          Confirmar
        </v-btn>
      </v-card-actions>
    </v-card>
    <v-alert v-if="alert" dense text type="success">
      {{ textAlert }}
    </v-alert>
  </div>
</template>

<script>
export default {
  name: "FormTasks",
  props: {
    task: {
      type: Object,
      default: () => {},
    },
    index: {
      type: Number,
      default: 0,
    },
    saveTask: {
      type: Function,
      default: () => {},
    },
  },
  data: () => ({
    alert: false,
    loading: false,
    selection: 1,
    inputPriority: false,
    inputTitle: "",
    inputDescription: "",
  }),
  methods: {
    readTask() {
      this.loading = true;
      this.textAlert = "¡Tarea agregada con éxito!";
      this.alert = true;
      setTimeout(() => {
        this.loading = false;
        this.alert = false;
        this.$props.saveTask(
          this.inputTitle,
          this.inputDescription,
          this.inputPriority
        );
        this.inputTitle = "";
        this.inputDescription = "";
        this.inputPriority = false;
        this.$refs.title.focus();
      }, 2000);
    },
  },
};
</script>