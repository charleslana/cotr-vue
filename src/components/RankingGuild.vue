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
      v-for="(item, index) in desserts"
      :key="item.name"
    >
      <td>{{ index + 1 }}</td>
      <td>{{ item.name }}</td>
      <td>{{ item.leader }}</td>
      <td>{{ item.totalMembers }}</td>
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
    totalMembers: 10,
  },
  {
    name: 'Ice cream sandwich',
    trophy: 237,
    leader: 'Ice cream sandwich',
    totalMembers: 10,
  },
  {
    name: 'Eclair',
    trophy: 262,
    leader: 'Eclair',
    totalMembers: 10,
  },
  {
    name: 'Cupcake',
    trophy: 305,
    leader: 'Cupcake',
    totalMembers: 10,
  },
  {
    name: 'Gingerbread',
    trophy: 356,
    leader: 'Gingerbread',
    totalMembers: 10,
  },
  {
    name: 'Jelly bean',
    trophy: 375,
    leader: 'Jelly bean',
    totalMembers: 10,
  },
  {
    name: 'Lollipop',
    trophy: 392,
    leader: 'Lollipop',
    totalMembers: 10,
  },
  {
    name: 'Honeycomb',
    trophy: 408,
    leader: 'Honeycomb',
    totalMembers: 10,
  },
  {
    name: 'Donut',
    trophy: 452,
    leader: 'Donut',
    totalMembers: 10,
  },
  {
    name: 'KitKat',
    trophy: 518,
    leader: 'KitKat',
    totalMembers: 10,
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
