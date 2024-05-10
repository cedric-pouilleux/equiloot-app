<template>
  <div class="galery">
    <div v-for="item in data">
      <img :src="item.pictureUrl" />
    </div>
  </div>
</template>

<script lang="ts" setup>
  import { useAsyncData } from "nuxt/app";
  import type { Item } from "~/types";

  const { data } = await useAsyncData<Item[]>(
    "items",
    () => $fetch("http://localhost:4000/items"),
    { server: false }
  );
</script>

<style scoped>
  .galery {
    display: flex;
    flex-wrap: wrap;
  }
  .galery > div {
    margin: 1px;
    border-radius: 3px;
  }
  .galery img {
    border-radius: 5px;
  }
</style>
