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
      v-for="(item, index) in items"
      :key="item.name"
    >
      <td>{{ index + 1 }}</td>
      <td>{{ item.name }}</td>
      <td>
        <img
          alt="Cristais Roxos"
          class="table-icon"
          src="@/assets/time_white.png"
        />
        {{ formatDuration(item.runDuration) }}
      </td>
    </tr>
    </tbody>
  </v-table>
</template>

<script lang="ts" setup>
import api from "@/config/axios-instance";

interface Item {
  name: string;
  runDuration: number;
}

const loading = ref(true);
const items = ref<Item[]>([]);
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
    const response = await api.get('/public/player/top-duration');
    items.value = response.data;
  } catch (err) {
    error.value = 'Erro ao buscar os dados.';
    console.error(err);
  } finally {
    loading.value = false;
  }
});
</script>
