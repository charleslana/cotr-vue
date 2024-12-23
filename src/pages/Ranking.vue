<template>
  <v-card>
    <v-tabs
      v-model="tab"
      bg-color=""
      align-tabs="center"
    >
      <v-tab value="ricos">Jogadores ricos</v-tab>
      <v-tab value="estilosos">Jogadores estilosos</v-tab>
      <v-tab value="avançados">Jogadores avançados</v-tab>
      <v-tab value="competidores">Jogadores competitivos</v-tab>
    </v-tabs>
    <v-card-text>
      <v-tabs-window v-model="tab">
        <v-tabs-window-item value="ricos">
          <small>O Resultado retorna os 100 melhores</small>
          <RankingRich />
        </v-tabs-window-item>
        <v-tabs-window-item value="estilosos">
          Two
        </v-tabs-window-item>
        <v-tabs-window-item value="avançados">
          Three
        </v-tabs-window-item>
        <v-tabs-window-item value="competitivos">
          Four
        </v-tabs-window-item>
      </v-tabs-window>
    </v-card-text>
  </v-card>
</template>

<script lang="ts" setup>
const tab = ref(null);
</script>

<style scoped>

</style>
