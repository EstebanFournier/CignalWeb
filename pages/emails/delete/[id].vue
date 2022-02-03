<template></template>

<script>
export default {
  data() {
    return {
      deleteMessage: "",
      id: "",
    };
  },

  // Supression de l'email en fonction de l'id 
  async mounted() {
    let auth = localStorage.getItem("Authorization");

    this.id = this.$route.params.id;

    var params = {
      method: "DELETE",
      headers: {
        "Content-Type": "application/json",
        Authorization: "Bearer " + auth,
      },
    };

    var apiURL = "http://localhost:8000/api/email/";

    fetch(apiURL + this.id, params)
      .then((response) => {
        this.deleteMessage = response.json();
      })
      .catch((error) => {
        console.log("error", error);
      })
      .finally(() => {
        this.$router.push("/emails/");
      });
  },
};
</script>

<style></style>
