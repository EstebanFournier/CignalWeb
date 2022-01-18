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
  data() {
    return {
      certificatData: "",
    };
  },

  async created() {
    let auth = localStorage.getItem("Authorization");

    var params = {
      method: "GET",
      headers: {
        "Content-Type": "application/json",
        Authorization: "Bearer " + auth,
      },
    };

    var apiURL = "http://localhost:8000/api/certificat";

    fetch(apiURL, params)
      .then((response) => response.json())
      .then((data) => {
        this.certificatData = data;
        //console.log("data", data);
        //console.log("certificatData", data.certificatData);
      });
  },
};
</script>
