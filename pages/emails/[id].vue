<template>
  <div>
    <TheHeader />
    <NavBar />
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

    var apiURL = "http://localhost:8000/api/email/";

    fetch(apiURL + this.id, params)
      .then((response) => response.json())
      .then((data) => {
        this.emailIdData = data;
        console.log("apiurl + id + params", apiURL + this.id, params);
        console.log("data", this.emailIdData);
      });
  },
};
</script>
