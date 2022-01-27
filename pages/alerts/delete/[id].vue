<template></template>

<script>
export default {
  data() {
    return {
      deleteMessage: "",
      id: "",
    };
  },

  async mounted() {
    let auth = localStorage.getItem("Authorization");
    //console.log("auth", auth);

    this.id = this.$route.params.id;
    //console.log("id", this.id);

    var params = {
      method: "DELETE",
      headers: {
        "Content-Type": "application/json",
        Authorization: "Bearer " + auth,
      },
    };
    //console.log("params", params);

    var apiURL = "http://localhost:8000/api/alert/";

    fetch(apiURL + this.id, params)
      .then((response) => {
        this.deleteMessage = response.json();
        //console.log("apiurl + id + params", apiURL + this.id, params);
        //console.log("data", this.deleteMessage);
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
