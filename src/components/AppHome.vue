<template>
  <v-carousel
    hide-delimiters
    style="height: 100vh;"
  >
    <v-carousel-item
      v-for="(item,i) in items"
      :key="i"
      :src="item.src"
      class="img-carousel"
    />
  </v-carousel>
  <v-container style="height: auto;">
    <v-card
      elevation="2"
    >
      <v-card-text class="text-center">
        <p class="text-h1">Crash On The Run está de volta</p>
      </v-card-text>
      <v-card-text class="text-center"></v-card-text>
    </v-card>
  </v-container>
  <v-parallax class="parallax"/>
</template>

<script lang="ts" setup>
const items = [
  {
    src: 'src/assets/bg_carousel.jpg',
  },
  {
    src: 'src/assets/bg_carousel_2.jpg',
  },
  {
    src: 'src/assets/bg_carousel_3.jpg',
  },
  {
    src: 'src/assets/bg_carousel_4.jpg',
  },
];
</script>

<style scoped>
.img-carousel {
  object-fit: cover;
  height: 100vh;
}

.parallax {
  background-image: url('../assets/bg_home.jpg');
  background-size:cover;
  min-height: 100vh;
  background-attachment: fixed;
  background-position: center;
  background-repeat: no-repeat;
}
</style>
