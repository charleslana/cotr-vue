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
      <td>{{ formatDuration(item.runDuration) }}</td>
    </tr>
    </tbody>
  </v-table>
</template>

<script lang="ts" setup>
import api from "@/config/axios-instance";

const desserts = [
  {
    name: 'Frozen Yogurt',
    runDuration: 'PT1M10.305S',
  },
  {
    name: 'Ice cream sandwich',
    runDuration: 'PT1H5M10S',
  },
  {
    name: 'Eclair',
    runDuration: 'PT5M10.305S',
  },
  {
    name: 'Cupcake',
    runDuration: 'PT3H5M10S',
  },
  {
    name: 'Gingerbread',
    runDuration: null,
  },
  {
    name: 'Jelly bean',
    runDuration: 'PT1M10.305S',
  },
  {
    name: 'Lollipop',
    runDuration: 'PT1M10.305S',
  },
  {
    name: 'Honeycomb',
    runDuration: 'PT1M10.305S',
  },
  {
    name: 'Donut',
    runDuration: 'PT1M10.305S',
  },
  {
    name: 'KitKat',
    runDuration: 'PT1M10.305S',
  },
];

const loading = ref(true);
const todos = ref<any[]>([]);
const error = ref<string | null>(null);

const formatDuration = (duration: string | null): string => {
  if (!duration) {
    return "0 horas, 0 minutos e 0 segundos";
  }
  const regex = /^PT(\d+)H(\d+)M(\d+(\.\d+)?)S$/;
  const match = duration.match(regex);
  if (match) {
    const hours = parseInt(match[1]);
    const minutes = parseInt(match[2]);
    const seconds = parseFloat(match[3]);
    return `${hours.toFixed(0)} horas, ${minutes.toFixed(0)} minutos e ${seconds.toFixed(2)} segundos`;
  }
  const regexWithoutHours = /^PT(\d+)M(\d+(\.\d+)?)S$/;
  const matchWithoutHours = duration.match(regexWithoutHours);
  if (matchWithoutHours) {
    const minutes = parseInt(matchWithoutHours[1]);
    const seconds = parseFloat(matchWithoutHours[2]);
    return `${minutes.toFixed(0)} minutos e ${seconds.toFixed(2)} segundos`;
  }
  return 'Duração inválida';
};


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
