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
        Nível
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
          src="@/assets/exp.png"
        />
        {{ item.level }}
      </td>
    </tr>
    </tbody>
  </v-table>
</template>

<script lang="ts" setup>
import api from "@/config/axios-instance";

interface Item {
  name: string;
  level: number;
}

const loading = ref(true);
const items = ref<Item[]>([]);
const error = ref<string | null>(null);

onMounted(async () => {
  try {
    const response = await api.get('/public/player/top-level');
    items.value = response.data;
  } catch (err) {
    error.value = 'Erro ao buscar os dados.';
    console.error(err);
  } finally {
    loading.value = false;
  }
});
</script>
