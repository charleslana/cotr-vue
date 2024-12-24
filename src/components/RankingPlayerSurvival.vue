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
        Tempo de sobrevivência
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
      <td>{{ item.survivalTime }}</td>
    </tr>
    </tbody>
  </v-table>
</template>

<script lang="ts" setup>
import api from "@/config/axios-instance";

const desserts = [
  {
    name: 'Frozen Yogurt',
    survivalTime: 159,
  },
  {
    name: 'Ice cream sandwich',
    survivalTime: 237,
  },
  {
    name: 'Eclair',
    survivalTime: 262,
  },
  {
    name: 'Cupcake',
    survivalTime: 305,
  },
  {
    name: 'Gingerbread',
    survivalTime: 356,
  },
  {
    name: 'Jelly bean',
    survivalTime: 375,
  },
  {
    name: 'Lollipop',
    survivalTime: 392,
  },
  {
    name: 'Honeycomb',
    survivalTime: 408,
  },
  {
    name: 'Donut',
    survivalTime: 452,
  },
  {
    name: 'KitKat',
    survivalTime: 518,
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
