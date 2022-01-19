<template>
  <div>
    <TheHeader />
    <NavBar />
    <form id="form" method="PUT">
      <div>
        <input
          id="nameAlert"
          name="nameAlert"
          type="text"
          value="nameAlert"
          class=""
          placeholder="Nom de l'alerte"
        />
      </div>
      <div>
        <input
          id="dateAlert"
          name="dateAlert"
          type="text"
          value="dateAlert"
          class=""
          placeholder="Date de l'alerte"
        />
      </div>
      <div>
        <input
          id="description"
          name="description"
          type="text"
          value="description"
          class=""
          placeholder="Description"
        />
      </div>
      <div>
        <br />
        <button class="" @click="submit" type="submit">Mettre à jour</button>
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
      inputNameAlert: "",
      inputDateAlert: "",
      inputDescription: "",
    };
  },

  async created() {
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
      .then((response) => response.json())
      .then((data) => {
        this.alertIdData = data;
        //console.log("apiurl + id + params", apiURL + this.id, params);
        //console.log("data", this.certificatIdData);
        const dataConnect = {
          projectName: (document.getElementById("nameAlert").value =
            this.alertIdData.nameAlert),
          dateAlert: (document.getElementById("dateAlert").value =
            this.alertIdData.dateAlert),
          description: (document.getElementById("description").value =
            this.alertIdData.description),
        };
        //console.log("ok", dataConnect);
      });
  },

  methods: {
    submit() {
      // Keep auth token for request
      let auth = localStorage.getItem("Authorization");
      //console.log("auth", auth);

      // Keep inputData in form for request
      const dataConnect = {
        nameAlert: document.getElementById("nameAlert").value,
        dateAlert: document.getElementById("dateAlert").value,
        description: document.getElementById("description").value,
      };
      console.log("ok2", dataConnect);

      // Creation of parameters for request
      var params = {
        method: "PUT",
        headers: {
          "Content-Type": "application/json",
          Authorization: "Bearer " + auth,
        },
        body: JSON.stringify(dataConnect),
      };
      //console.log("params", params);

      var apiURL = "http://localhost:8000/api/email/";

      fetch(apiURL + this.id, params).then((response) => response.json());
      /* .then((data) => {
          this.certificatIdData = data;
        }); */
      console.log("apiurl + id + params", apiURL + this.id, params);
      //console.log("data", this.certificatIdData);
      this.$router.push("/emails/");
    },
  },
};
</script>
