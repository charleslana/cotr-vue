<template>
  <small>O Resultado retorna os 100 melhores</small>
  <v-skeleton-loader v-if="loading" type="table"></v-skeleton-loader>
  <v-table v-else>
    <thead>
    <tr>
      <th class="text-left">
        Posição
      </th>
      <th class="text-left">
        Nome
      </th>
      <th class="text-left">
        Líder
      </th>
      <th class="text-left">
        Total de membros
      </th>
      <th class="text-left">
        Troféus
      </th>
    </tr>
    </thead>
    <tbody>
    <tr
      v-for="(item, index) in items"
      :key="item.guildName"
    >
      <td>{{ index + 1 }}</td>
      <td>{{ item.guildName }}</td>
      <td>{{ item.leaderName }}</td>
      <td>{{ item.totalMembers }} / 30</td>
      <td>
        <img
          alt="Cristais Roxos"
          class="table-icon"
          src="@/assets/trophy_guild.png"
        />
        {{ formatNumber(item.totalTrophies) }}
      </td>
    </tr>
    </tbody>
  </v-table>
</template>

<script lang="ts" setup>
import api from "@/config/axios-instance";
import {formatNumber} from "@/utils/utils";

interface Item {
  guildName: string;
  totalTrophies: number;
  totalMembers: number;
  leaderName: string;
}

const loading = ref(true);
const items = ref<Item[]>([]);
const error = ref<string | null>(null);

onMounted(async () => {
  try {
    const response = await api.get('/public/guild/top-trophies');
    items.value = response.data;
  } catch (err) {
    error.value = 'Erro ao buscar os dados.';
    console.error(err);
  } finally {
    loading.value = false;
  }
});
</script>
