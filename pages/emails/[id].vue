<template>
  <div>
    <TheHeader title="Emails" />
    <h1>
      {{ emailIdData.id }}
    </h1>
    <h2>
      {{ emailIdData.email }}
    </h2>
    <h3>
      {{ emailIdData.certificat_id }}
    </h3>
  </div>
</template>

<script>
export default {
  data() {
    return {
      emailIdData: "",
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

    var apiURL = "http://localhost:8000/api/email/";

    fetch(apiURL + this.id, params)
      .then((response) => response.json())
      .then((response) => {
        this.emailIdData = response;
      })
      .catch((error) => {
        console.log("error", error);
      });
  },
};
</script>
