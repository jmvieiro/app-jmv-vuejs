<template>
  <div>
    <v-form ref="form" v-model="valid" lazy-validation>
      <v-card :loading="loading" class="mx-auto my-12">
        <v-card-title>Agregar contacto</v-card-title>

        <v-card-text>
          <v-text-field
            class="mb-4"
            ref="name"
            v-model="model.name"
            :rules="titleRules"
            label="Nombre"
            required
            :counter="15"
          ></v-text-field>
          <v-text-field
            class="mb-4"
            v-model="model.phone"
            :rules="phoneRules"
            label="Teléfono"
            required
            type="number"
            :counter="10"
          ></v-text-field>
          <v-text-field
            class="mb-4"
            v-model="model.email"
            :rules="emailRules"
            label="Email"
            required
            :counter="25"
          ></v-text-field>

          <v-checkbox
            v-model="model.terms"
            :rules="termsRules"
            id="inputTerms"
            :label="`Términos y condiciones`"
          ></v-checkbox>
        </v-card-text>

        <v-divider class="mx-4 my-4"></v-divider>

        <v-card-actions class="mx-2">
          <v-row>
            <v-col lg="3">
              <v-btn color="primary lighten-1 mb-2" @click="validate">
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
    </v-form>
  </div>
</template>

<script>
export default {
  name: "FormContact",
  data: () => ({
    valid: true,
    alert: false,
    loading: false,
    inputPriority: false,
    model: {
      name: "",
      phone: 0,
      email: "",
      terms: false,
    },
    titleRules: [
      (v) => !!v || "Nombre es obligatorio.",
      (v) =>
        (v && v.length <= 15) ||
        "El nombre no debe contener más de 15 caracteres.",
    ],
    emailRules: [
      (v) => !!v || "Email es obligatorio.",
      (v) => /.+@.+\..+/.test(v) || "Ingresa un email válido.",
      (v) =>
        (v && v.length <= 25) ||
        "El email no debe contener más de 25 caracteres.",
    ],
    phoneRules: [
      (v) => !!v || "Teléfono es obligatorio.",
      (v) => (v && v > 0) || "El teléfono debe ser mayor a 0.",
      (v) =>
        (v && v.length <= 10) ||
        "El teléfono no debe contener más de 10 caracteres.",
    ],
    termsRules: [(v) => !!v || "Tenés que aceptar los términos y condiciones."],
  }),
  methods: {
    validate() {
      if (this.$refs.form.validate()) this.readContact();
    },
    readContact() {
      this.loading = true;
      this.textAlert = "¡Contacto agregado con éxito!";
      this.alert = true;
      setTimeout(() => {
        this.loading = false;
        this.alert = false;
        this.$emit("saveContact", this.model);
        this.model.name = "";
        this.model.phone = 0;
        this.model.email = "";
        this.inputTerms = false;
        this.$refs.name.focus();
      }, 1000);
    },
  },
};
</script>