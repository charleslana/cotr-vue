<template>
  <v-app-bar
    absolute
    color="white"
    elevation="0"
  >
    <v-app-bar-nav-icon @click="toggleDrawer" v-if="isMobile"/>
    <v-toolbar-title>Crash On The Run Revival Project</v-toolbar-title>
    <v-spacer/>
    <!-- Links visíveis em telas grandes (desktop) -->
    <v-row v-if="!isMobile" align="center">
      <v-btn to="/">Home</v-btn>
      <v-btn to="/about">Sobre</v-btn>
      <v-btn to="/ranking">Classificação de Jogadores</v-btn>
      <v-btn to="/redeem">Resgatar código</v-btn>
    </v-row>
    <v-spacer/>
    <!-- Menu para mobile -->
<!--    <v-menu v-if="isMobile" v-model="menuVisible" bottom left>-->
<!--      <v-list>-->
<!--        <v-list-item to="/">-->
<!--          <v-list-item-title>Home</v-list-item-title>-->
<!--        </v-list-item>-->
<!--        <v-list-item to="/about">-->
<!--          <v-list-item-title>About</v-list-item-title>-->
<!--        </v-list-item>-->
<!--      </v-list>-->
<!--    </v-menu>-->
  </v-app-bar>
  <!-- Menu de navegação para mobile (drawer) -->
  <v-navigation-drawer
    v-model="drawer"
    absolute
    temporary
    right
    app
  >
    <v-list nav dense>
      <v-list-item to="/">
        <v-icon>mdi-home</v-icon>
        <v-list-item-title>Home</v-list-item-title>
      </v-list-item>

      <v-list-item to="/about">
        <v-icon>mdi-information</v-icon>
        <v-list-item-title>Sobre</v-list-item-title>
      </v-list-item>

      <v-list-item to="/ranking">
        <v-icon>mdi-trophy</v-icon>
        <v-list-item-title>Classificação de Jogadores</v-list-item-title>
      </v-list-item>

      <v-list-item to="/redeem">
        <v-icon>mdi-gift</v-icon>
        <v-list-item-title>Resgatar código</v-list-item-title>
      </v-list-item>
    </v-list>
  </v-navigation-drawer>
</template>

<script lang="ts" setup>
import { ref } from 'vue';

const drawer = ref(false);

// const menuVisible = ref(false);

const isMobile = ref(window.innerWidth <= 600);

// const isMobile = computed(() => {
//   return window.innerWidth <= 600;
// });

// const toggleMenu = () => {
//   menuVisible.value = !menuVisible.value;
// };

const updateIsMobile = () => {
  isMobile.value = window.innerWidth <= 600;
};

const toggleDrawer = () => {
  drawer.value = !drawer.value;
};

onMounted(() => {
  window.addEventListener('resize', updateIsMobile);
});

// Remover o evento de resize no beforeUnmount
onBeforeUnmount(() => {
  window.removeEventListener('resize', updateIsMobile);
});
</script>

<style>

</style>
