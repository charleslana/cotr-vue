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
      <td>{{ item.leader }}</td>
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
    leader: 'Frozen Yogurt',
  },
  {
    name: 'Ice cream sandwich',
    trophy: 237,
    leader: 'Ice cream sandwich',
  },
  {
    name: 'Eclair',
    trophy: 262,
    leader: 'Eclair',
  },
  {
    name: 'Cupcake',
    trophy: 305,
    leader: 'Cupcake',
  },
  {
    name: 'Gingerbread',
    trophy: 356,
    leader: 'Gingerbread',
  },
  {
    name: 'Jelly bean',
    trophy: 375,
    leader: 'Jelly bean',
  },
  {
    name: 'Lollipop',
    trophy: 392,
    leader: 'Lollipop',
  },
  {
    name: 'Honeycomb',
    trophy: 408,
    leader: 'Honeycomb',
  },
  {
    name: 'Donut',
    trophy: 452,
    leader: 'Donut',
  },
  {
    name: 'KitKat',
    trophy: 518,
    leader: 'KitKat',
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
