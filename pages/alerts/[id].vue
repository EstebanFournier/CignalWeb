<template>
  <div>
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

  async created() {
    let auth = localStorage.getItem("Authorization");
    console.log("auth", auth);

    this.id = this.$route.params.id;
    console.log("id", this.id);

    var params = {
      method: "GET",
      headers: {
        "Content-Type": "application/json",
        Authorization: "Bearer " + auth,
      },
    };
    console.log("params", params);

    var apiURL = "http://localhost:8000/api/alert/";

    fetch(apiURL + this.id, params)
      .then((response) => response.json())
      .then((data) => {
        this.alertIdData = data;
        console.log("apiurl + id + params", apiURL + this.id, params);
        console.log("data", this.alertIdData);
      });
  },
};
</script>
