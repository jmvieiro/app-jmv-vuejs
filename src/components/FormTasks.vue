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
        <v-row>
          <v-col lg="3">
            <v-btn color="primary lighten-1 mb-2" @click="readTask">
              Confirmar
            </v-btn>
          </v-col>
          <v-col lg="9">
            <v-alert v-if="alert" dense text type="success" class="mb-0">
              {{ textAlert }}
            </v-alert>
          </v-col>
        </v-row>
      </v-card-actions>
    </v-card>
  </div>
</template>

<script>
export default {
  name: "FormTasks",
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
        this.$emit("saveTask", {
          title: this.inputTitle,
          description: this.inputDescription,
          priority: this.inputPriority,
        });
        this.inputTitle = "";
        this.inputDescription = "";
        this.inputPriority = false;
        this.$refs.title.focus();
      }, 1000);
    },
  },
};
</script>