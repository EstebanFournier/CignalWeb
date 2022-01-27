<template>
  <div>
    <TheHeader />
    <NavBar />
    <form id="form" method="PUT" @submit="submit">
      <div>
        <input
          id="nameAlert"
          name="nameAlert"
          type="text"
          v-model="alertIdData.nameAlert"
          class=""
          placeholder="Nom de l'alerte"
        />
      </div>
      <div>
        <input
          id="dateAlert"
          name="dateAlert"
          type="text"
          v-model="alertIdData.dateAlert"
          class=""
          placeholder="Date de l'alerte"
        />
      </div>
      <div>
        <input
          id="description"
          name="description"
          type="text"
          v-model="alertIdData.description"
          class=""
          placeholder="Description"
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
      alertIdData: "",
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

    var apiURL = "http://localhost:8000/api/alert/";

    fetch(apiURL + this.id, params)
      .then((response) => {
        this.alertIdData = response.json();
        //console.log("apiurl + id + params", apiURL + this.id, params);
        //console.log("data", this.certificatIdData);
      })
      .catch((error) => {
        console.log("erroe", error);
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
        body: JSON.stringify(this.alertIdData),
      };
      //console.log("params", params);

      var apiURL = "http://localhost:8000/api/email/";

      fetch(apiURL + this.id, params)
        .then((response) => response.json())
        .catch((error) => {
          console.log("error", error);
        })
        .finally(() => {
          return this.$router.push("/alerts/");
        });

      console.log("apiurl + id + params", apiURL + this.id, params);
    },
  },
};
</script>
