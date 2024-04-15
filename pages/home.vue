<template>
  <div class="center">
    <h1>equiloot</h1>
    <pre>
      {{status}}
      {{data}}
      {{pending}}
      {{error}}
    </pre>
  </div>
</template>

<script lang="ts" setup>
import {useAsyncData} from "nuxt/app";

const { data, pending, error, status } = await useAsyncData(
    'items',
    () => $fetch('http://localhost:4000/items'),
    { server: false }
);

</script>
