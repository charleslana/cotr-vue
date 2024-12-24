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
        Joias do Poder
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
      <td>{{ item.powerGems }}</td>
    </tr>
    </tbody>
  </v-table>
</template>

<script lang="ts" setup>
import api from "@/config/axios-instance";

const desserts = [
  {
    name: 'Frozen Yogurt',
    powerGems: 159,
  },
  {
    name: 'Ice cream sandwich',
    powerGems: 237,
  },
  {
    name: 'Eclair',
    powerGems: 262,
  },
  {
    name: 'Cupcake',
    powerGems: 305,
  },
  {
    name: 'Gingerbread',
    powerGems: 356,
  },
  {
    name: 'Jelly bean',
    powerGems: 375,
  },
  {
    name: 'Lollipop',
    powerGems: 392,
  },
  {
    name: 'Honeycomb',
    powerGems: 408,
  },
  {
    name: 'Donut',
    powerGems: 452,
  },
  {
    name: 'KitKat',
    powerGems: 518,
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
