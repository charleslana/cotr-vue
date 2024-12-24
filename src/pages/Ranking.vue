<template>
  <v-card>
    <v-tabs
      v-model="tab"
      align-tabs="center"
      bg-color=""
      show-arrows
    >
      <v-tab value="ricos">Jogadores ricos</v-tab>
      <v-tab value="estilosos">Jogadores estilosos</v-tab>
      <v-tab value="experientes">Jogadores experientes</v-tab>
      <v-tab value="avançados">Jogadores avançados</v-tab>
      <v-tab value="competitivos">Jogadores competitivos</v-tab>
      <v-tab value="desafiadores">Jogadores desafiadores</v-tab>
      <v-tab value="guildas">Melhores guildas</v-tab>
    </v-tabs>
    <v-card-text>
      <v-tabs-window v-model="tab">
        <v-tabs-window-item value="ricos">
          <RankingPlayerRich/>
        </v-tabs-window-item>
        <v-tabs-window-item value="estilosos">
          <RankingPlayerSkin/>
        </v-tabs-window-item>
        <v-tabs-window-item value="experientes">
          <RankingPlayerLevel/>
        </v-tabs-window-item>
        <v-tabs-window-item value="avançados">
          <RankingPlayerPowerGems/>
        </v-tabs-window-item>
        <v-tabs-window-item value="competitivos">
          <RankingPlayerTrophy/>
        </v-tabs-window-item>
        <v-tabs-window-item value="desafiadores">
          <RankingPlayerSurvival/>
        </v-tabs-window-item>
        <v-tabs-window-item value="guildas">
          <RankingGuild/>
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
