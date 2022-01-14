<template>
  <div>
    <h1>
      {{certificatIdData}}
    </h1>
  </div>
</template>

<script>
export default {
  data: () => ({
    certificatIdData: {},
    id: 0,
  }),

  created() {
    console.log("route:", this.$route.params);
    this.id = this.$route.params.id;
    console.log('id:', this.id);
  },

  async mounted() {
    const apiURL = `http://localhost:8000/api/certificat/`;
    console.log('url:', apiURL + this.id);

    const response = await fetch(apiURL + this.id).then((data) => data.json());

    this.certificatIdData = response;
    console.log('response', response)
  },
};
</script>