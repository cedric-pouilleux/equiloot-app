<template>
  <UContainer>
    <h1 class="text-lg">App configurations</h1>
    <p>{{ marker }}</p>
    <div v-if="loading">Loading ...</div>

    <h2 class="text-base font-normal">Data extract and populate</h2>
    <div class="flex">
      <div class="flex-1">
        <UCheckbox
          label="Profondeur de brassenoire"
          v-model="selector"
          :value="{
            name: 'profondeurs-de-brassenoire',
            url: 'https://www.wowhead.com/classic/fr/zone=719/profondeurs-de-brassenoire',
          }"
        />
        <UCheckbox
          label="Gnomeregan"
          v-model="selector"
          :value="{
            name: 'gnomeregan',
            url: 'https://www.wowhead.com/classic/fr/zone=721/gnomeregan',
          }"
        />
        <UCheckbox
          label="Le temple D'Atal'Hakkar"
          v-model="selector"
          :value="{
            name: 'le-temple-datalhakkar',
            ur: 'https://www.wowhead.com/classic/fr/zone=1477/le-temple-datalhakkar',
          }"
        />
        <UButton @click="handleExtractData">Extract</UButton>
      </div>
    </div>
  </UContainer>
</template>

<script setup lang="ts">
  const selector = ref([]);
  const marker = ref<string>();
  const loading = ref<boolean>(false);

  const links = ref([
    {
      label: "Installation",
      icon: "i-heroicons-home",
      to: "/getting-started/installation",
    },
  ]);

  async function handleExtractData() {
    loading.value = true;
    const { data, pending } = await useFetch("http://localhost:4000/extract", {
      method: "POST",
      body: JSON.stringify({ dungeons: selector.value, uploadPictures: true }),
    });
    marker.value = data.value as string;
    loading.value = pending.value;
  }
</script>

<style scoped lang="scss"></style>
