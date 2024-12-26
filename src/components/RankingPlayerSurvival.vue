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
    runDuration: 70.305,
  },
  {
    name: 'Ice cream sandwich',
    runDuration: 70.305,
  },
  {
    name: 'Eclair',
    runDuration: 7200.150,
  },
  {
    name: 'Cupcake',
    runDuration: 130.305,
  },
  {
    name: 'Gingerbread',
    runDuration: null,
  },
  {
    name: 'Jelly bean',
    runDuration: null,
  },
  {
    name: 'Lollipop',
    runDuration: null,
  },
  {
    name: 'Honeycomb',
    runDuration: null,
  },
  {
    name: 'Donut',
    runDuration: null,
  },
  {
    name: 'KitKat',
    runDuration: null,
  },
];

const loading = ref(true);
const todos = ref<any[]>([]);
const error = ref<string | null>(null);

const formatDuration = (seconds: number | null): string => {
  if (seconds === null || seconds < 0) {
    return "0 horas, 0 minutos e 0 segundos";
  }
  const hours = Math.floor(seconds / 3600);
  const remainingSecondsAfterHours = seconds % 3600;
  const minutes = Math.floor(remainingSecondsAfterHours / 60);
  const remainingSeconds = Math.floor(remainingSecondsAfterHours % 60);
  const parts = [];
  if (hours > 0) parts.push(`${hours} ${hours === 1 ? 'hora' : 'horas'}`);
  if (minutes > 0) parts.push(`${minutes} ${minutes === 1 ? 'minuto' : 'minutos'}`);
  if (remainingSeconds > 0 || parts.length === 0) parts.push(`${remainingSeconds} ${remainingSeconds === 1 ? 'segundo' : 'segundos'}`);
  return parts.join(', ').replace(/, ([^,]*)$/, ' e $1');
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
