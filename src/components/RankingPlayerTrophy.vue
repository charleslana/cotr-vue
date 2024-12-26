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
        Jogador
      </th>
      <th class="text-left">
        Troféus
      </th>
    </tr>
    </thead>
    <tbody>
    <tr
      v-for="(item, index) in items"
      :key="item.name"
    >
      <td>{{ index + 1 }}</td>
      <td>{{ item.name }}</td>
      <td>
        <img
          alt="Cristais Roxos"
          class="table-icon"
          src="@/assets/trophy.png"
        />
        {{ formatNumber(item.crashPointsEarned) }}
      </td>
    </tr>
    </tbody>
  </v-table>
</template>

<script lang="ts" setup>
import api from "@/config/axios-instance";
import {formatNumber} from "@/utils/utils";

interface Item {
  name: string;
  crashPointsEarned: number;
}

const loading = ref(true);
const items = ref<Item[]>([]);
const error = ref<string | null>(null);

onMounted(async () => {
  try {
    const response = await api.get('/public/player/top-points');
    items.value = response.data;
  } catch (err) {
    error.value = 'Erro ao buscar os dados.';
    console.error(err);
  } finally {
    loading.value = false;
  }
});
</script>
