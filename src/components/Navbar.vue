<template>
  <div>
    <v-app-bar app color="deep-purple accent-4" dense dark>
      <v-app-bar-nav-icon @click="drawer = true"></v-app-bar-nav-icon>
      <v-toolbar-title>Iniciando Vue/CLI</v-toolbar-title>
      <v-spacer></v-spacer>
    </v-app-bar>

    <v-navigation-drawer v-model="drawer" absolute temporary>
      <v-list nav dense>
        <v-list-item-group
          v-model="group"
          active-class="deep-purple--text text--accent-4"
        >
          <v-list-item @click="showItem(1)">
            <v-list-item-icon>
              <v-icon>mdi-numeric</v-icon>
            </v-list-item-icon>
            <v-list-item-title>Desafío 1: Contador</v-list-item-title>
          </v-list-item>

          <v-list-item @click="showItem(2)">
            <v-list-item-icon>
              <v-icon>mdi-calendar-check</v-icon>
            </v-list-item-icon>
            <v-list-item-title>Desafío 2: App tareas</v-list-item-title>
          </v-list-item>

          <v-list-item @click="showItem(3)">
            <v-list-item-icon>
              <v-icon>mdi-calendar-check</v-icon>
            </v-list-item-icon>
            <v-list-item-title> Desafío 3: App tareas Cli</v-list-item-title>
          </v-list-item>
        </v-list-item-group>
      </v-list>
    </v-navigation-drawer>
  </div>
</template>

<script>
export default {
  data: () => ({
    drawer: false,
    group: null,
  }),
  methods: {
    showItem(item) {
      this.$emit("showItem", item);
    },
  },
};
</script>