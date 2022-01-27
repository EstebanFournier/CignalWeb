<template>
  <div>
    <TheHeader />
    <NavBar />
    <form id="form" method="PUT" @submit="submit">
      <div>
        <input
          id="projectName"
          name="projectName"
          type="text"
          v-model="certificatIdData.projectName"
          class=""
          placeholder="Nom du certificat"
        />
      </div>
      <div>
        <input
          id="type"
          name="type"
          type="text"
          v-model="certificatIdData.type"
          class=""
          placeholder="Type de certificat"
        />
      </div>
      <div>
        <input
          id="plateform"
          name="plateform"
          type="text"
          v-model="certificatIdData.plateform"
          class=""
          placeholder="Nom de la plateforme"
        />
      </div>
      <div>
        <input
          id="description"
          name="description"
          type="text"
          v-model="certificatIdData.description"
          class=""
          placeholder="Description"
        />
      </div>
      <div>
        <input
          id="startDate"
          name="startDate"
          type="date"
          v-model="certificatIdData.startDate"
          class=""
          placeholder="Date de début"
        />
      </div>
      <div>
        <input
          id="endDate"
          name="endDate"
          type="date"
          v-model="certificatIdData.endDate"
          class=""
          placeholder="Date de fin"
        />
      </div>
      <div>
        <br />
        <button class="" type="submit">Mettre à jour</button>
      </div>
    </form>
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

    fetch(apiURL + this.id, params).then((response) => {
      this.certificatIdData = response.json();
      //console.log("apiurl + id + params", apiURL + this.id, params);
      //console.log("data", this.certificatIdData);
    });
  },

  methods: {
    submit(e) {
      e.preventDefault();

      // Keep auth token for request
      let auth = localStorage.getItem("Authorization");
      //console.log("auth", auth);

      // Creation of parameters for request
      var params = {
        method: "PUT",
        headers: {
          "Content-Type": "application/json",
          Authorization: "Bearer " + auth,
        },
        body: JSON.stringify(this.certificatIdData),
      };
      //console.log("params", params);

      var apiURL = "http://localhost:8000/api/certificat/";

      fetch(apiURL + this.id, params)
        .then((response) => response.json())
        .catch((error) => {
          console.log("error", error);
        })
        .finally(() => {
          this.$router.push("/certificats/");
        });
      console.log("apiurl + id + params", apiURL + this.id, params);
    },
  },
};
</script>
