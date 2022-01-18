<template>
  <div>
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
/* export default {
  data: () => ({
    certificatIdData: {},
    id: 0,
  }),

  created() {
    console.log("route:", this.$route.params);
    this.id = this.$route.params.id;
    console.log('id:', this.id);
  },

  async mounted() {
    const apiURL = `http://localhost:8000/api/certificat/`;
    console.log('url:', apiURL + this.id);

    const response = await fetch(apiURL + this.id).then((data) => data.json());

    this.certificatIdData = response;
    console.log('response', response)
  },
}; */

export default {
  data() {
    return {
      certificatIdData: "",
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

    var apiURL = "http://localhost:8000/api/certificat/";

    fetch(apiURL + this.id, params)
      .then((response) => response.json())
      .then((data) => {
        this.certificatIdData = data;
        console.log("apiurl + id + params", apiURL + this.id, params);
        console.log("data", this.certificatIdData);
      });
  },
};
</script>
