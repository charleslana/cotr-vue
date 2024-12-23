<template>
  <v-table>
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
      <td>{{ item.crystals }}</td>
    </tr>
    </tbody>
  </v-table>
</template>

<script lang="ts" setup>
const desserts = [
  {
    name: 'Frozen Yogurt',
    crystals: 159,
  },
  {
    name: 'Ice cream sandwich',
    crystals: 237,
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
</script>
