<template>
  <v-app>
    <v-app-bar app dense>
      <v-app-bar-nav-icon @click='drawer = true'></v-app-bar-nav-icon>
      <v-app-bar-title>Tasks List</v-app-bar-title>
    </v-app-bar>

    
    <v-navigation-drawer app
    v-model="drawer"
    absolute
    temporary
    style='background-color: #ededed'
    >
      <v-layout column align-center mt-2>
        <v-flex>
            <v-avatar>
                <img src="@/assets/perfil-recortado.jpeg" alt="Mauro Arias">
            </v-avatar>
        </v-flex>
        <v-flex>
            <a href="https://mauro-arias.com.ar"><p class='mt-3 text-caption'>Desarrollado por Mauro Arias</p></a> 
        </v-flex>
      </v-layout>
    </v-navigation-drawer>

    <v-main>
      <router-view/>
    </v-main>
  </v-app>
</template>

<script>

export default {
  name: 'App',

  data: () => ({
    drawer: false
  }),
};
</script>
