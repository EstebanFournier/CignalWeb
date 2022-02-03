<template>
  <div>
    <TheHeader title="Certificats"></TheHeader>
    <h1>
      {{ certificatIdData.id }}
    </h1>
    <h2>
      {{ certificatIdData.projectName }}
    </h2>
    <h3>
      {{ certificatIdData.description }}
    </h3>
  </div>
</template>

<script>
export default {
  data() {
    return {
      certificatIdData: "",
      id: "",
    };
  },

  // Récupération des données en fonction de l'id
  async mounted() {
    let auth = localStorage.getItem("Authorization");

    this.id = this.$route.params.id;

    var params = {
      method: "GET",
      headers: {
        "Content-Type": "application/json",
        Authorization: "Bearer " + auth,
      },
    };

    var apiURL = "http://localhost:8000/api/certificat/";

    fetch(apiURL + this.id, params)
      .then((response) => response.json())
      .then((response) => {
        this.certificatIdData = response;
      })
      .catch((error) => {
        console.log("error", error);
      });
  },
};
</script>
