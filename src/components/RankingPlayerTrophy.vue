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
      v-for="(item, index) in desserts"
      :key="item.name"
    >
      <td>{{ index + 1 }}</td>
      <td>{{ item.name }}</td>
      <td>{{ item.trophy }}</td>
    </tr>
    </tbody>
  </v-table>
</template>

<script lang="ts" setup>
import api from "@/config/axios-instance";

const desserts = [
  {
    name: 'Frozen Yogurt',
    trophy: 159,
  },
  {
    name: 'Ice cream sandwich',
    trophy: 237,
  },
  {
    name: 'Eclair',
    trophy: 262,
  },
  {
    name: 'Cupcake',
    trophy: 305,
  },
  {
    name: 'Gingerbread',
    trophy: 356,
  },
  {
    name: 'Jelly bean',
    trophy: 375,
  },
  {
    name: 'Lollipop',
    trophy: 392,
  },
  {
    name: 'Honeycomb',
    trophy: 408,
  },
  {
    name: 'Donut',
    trophy: 452,
  },
  {
    name: 'KitKat',
    trophy: 518,
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
