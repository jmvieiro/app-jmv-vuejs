<template>
  <div>
    <v-card flat>
      <v-card-text>
        <h2>Listado de contactos</h2>
        <v-row v-if="contacts.length === 0">
          <v-col>
            <div class="mx-auto my-3 text-center d-block">
              <v-alert color="primary lighten-2" dark
                >¡No tenés contactos agendados!</v-alert
              >
            </div>
          </v-col>
        </v-row>
        <v-row v-else>
          <v-col>
            <v-data-table
              :headers="headers"
              :items="contacts"
              style="margin: 0 auto; width: 98%; max-width: 98%"
              class="elevation-2 mt-6"
            >
            </v-data-table>
          </v-col>
        </v-row>
      </v-card-text>
    </v-card>
  </div>
</template>

<script>
export default {
  name: "ListContacts",
  data: () => {
    return {
      headers: [
        { text: "ID", align: "start", value: "id" },
        { text: "Nombre", value: "name" },
        { text: "Teléfono", value: "phone" },
        { text: "EmailF", value: "email" },
      ],
    };
  },
  props: {
    contacts: {
      type: Array,
      default: () => [],
    },
  },
};
</script>