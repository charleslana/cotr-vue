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
        Cristais Roxos
      </th>
    </tr>
    </thead>
    <tbody>
    <tr
      v-for="(item, index) in desserts"
      :key="item.name"
    >
      <td>{{ index + 1 }}</td>
      <td>{{ item.name }}</td>
      <td>{{ formatNumber(item.crystals) }}</td>
    </tr>
    </tbody>
  </v-table>
</template>

<script lang="ts" setup>
import {formatNumber} from "@/utils/utils";
import api from "@/config/axios-instance";

const desserts = [
  {
    name: 'Frozen Yogurt',
    crystals: 1599,
  },
  {
    name: 'Ice cream sandwich',
    crystals: 23777,
  },
  {
    name: 'Eclair',
    crystals: 262,
  },
  {
    name: 'Cupcake',
    crystals: 305,
  },
  {
    name: 'Gingerbread',
    crystals: 356,
  },
  {
    name: 'Jelly bean',
    crystals: 375,
  },
  {
    name: 'Lollipop',
    crystals: 392,
  },
  {
    name: 'Honeycomb',
    crystals: 408,
  },
  {
    name: 'Donut',
    crystals: 452,
  },
  {
    name: 'KitKat',
    crystals: 518,
  },
];

const loading = ref(true);
const todos = ref<any[]>([]);
const error = ref<string | null>(null);

onMounted(async () => {
  try {
    const response = await api.get('/todos');
    todos.value = response.data;
    console.log(todos.value);
  } catch (err) {
    error.value = 'Erro ao buscar os todos.';
    console.error(err);
  } finally {
    loading.value = false;
  }
});
</script>
