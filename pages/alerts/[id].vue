<template>
  <div>
    <TheHeader title="Alertes"></TheHeader>
    <h1>
      {{ alertIdData.id }}
    </h1>
    <h2>
      {{ alertIdData.projectName }}
    </h2>
    <h3>
      {{ alertIdData.description }}
    </h3>
  </div>
</template>

<script>
export default {
  data() {
    return {
      alertIdData: "",
      id: "",
    };
  },

  // Récupération des données par id
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

    var apiURL = "http://localhost:8000/api/alert/";

    fetch(apiURL + this.id, params)
      .then((response) => response.json())
      .then((response) => {
        this.alertIdData = response;
      })
      .catch((error) => {
        console.log("error", error);
      });
  },
};
</script>
