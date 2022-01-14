<template>
  <div>
    <div class="mt-4" v-for="certificat in certificatData" :key="certificat.id">
      <NuxtLink :to="`/certificats/${certificat.id}`">
        <br />
        <h1>
          {{ certificat.id }}
        </h1>
        <h2>
          {{ certificat.projectName }}
        </h2>
        <p>
          {{ certificat.description }}
        </p>
      </NuxtLink>
    </div>
  </div>
</template>

<script>
export default {
  data: () => ({
    certificatData: {},
  }),
  id: 2,

  async created() {
    const apiURL = "http://localhost:8000/api/certificat/";

    const response = await fetch(apiURL).then(
      (data) => data.json());

    this.certificatData = response;
  },
};
</script>