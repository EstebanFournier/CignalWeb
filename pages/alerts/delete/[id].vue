<template></template>

<script>
export default {
  data() {
    return {
      deleteMessage: "",
      id: "",
    };
  },

  // Appel de la route delete alert
  async mounted() {
    // Récupération du token d'authentification
    let auth = localStorage.getItem("Authorization");

    // Récupération de l'id dans l'url
    this.id = this.$route.params.id;

    // Création des paramètres de la requête
    var params = {
      method: "DELETE",
      headers: {
        "Content-Type": "application/json",
        Authorization: "Bearer " + auth,
      },
    };

    // URL de la requête
    var apiURL = "http://localhost:8000/api/alert/";

    // Execution de la requête
    fetch(apiURL + this.id, params)
      .then((response) => {
        this.deleteMessage = response.json();
      })
      .catch((error) => {
        console.log("error", error);
      })
      .finally(() => {
        this.$router.push("/alerts/");
      });
  },
};
</script>
