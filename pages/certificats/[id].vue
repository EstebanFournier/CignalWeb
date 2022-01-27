<template>
  <div>
    <TheHeader />
    <NavBar />
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

  async mounted() {
    let auth = localStorage.getItem("Authorization");
    //console.log("auth", auth);

    this.id = this.$route.params.id;
    //console.log("id", this.id);

    var params = {
      method: "GET",
      headers: {
        "Content-Type": "application/json",
        Authorization: "Bearer " + auth,
      },
    };
    //console.log("params", params);

    var apiURL = "http://localhost:8000/api/certificat/";

    fetch(apiURL + this.id, params)
      .then((response)=> response.json())
      .then((response) => {
        this.certificatIdData = response;
        //console.log("apiurl + id + params", apiURL + this.id, params);
        //console.log("data", this.certificatIdData);
      })
      .catch((error) => {
        console.log("error", error);
      });
  },
};
</script>
