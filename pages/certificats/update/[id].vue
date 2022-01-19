<template>
  <div>
    <TheHeader />
    <NavBar />
    <form id="form" method="PUT">
      <div>
        <input
          id="projectName"
          name="projectName"
          type="text"
          value="projectName"
          class=""
          placeholder="Nom du certificat"
        />
      </div>
      <div>
        <input
          id="type"
          name="type"
          type="text"
          value="type"
          class=""
          placeholder="Type de certificat"
        />
      </div>
      <div>
        <input
          id="plateform"
          name="plateform"
          type="text"
          value="plateform"
          class=""
          placeholder="Nom de la plateforme"
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
        <input
          id="startDate"
          name="startDate"
          type="date"
          value="startDate"
          class=""
          placeholder="Date de début"
        />
      </div>
      <div>
        <input
          id="endDate"
          name="endDate"
          type="date"
          value="endDate"
          class=""
          placeholder="Date de fin"
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
      certificatIdData: "",
      id: "",
      inputEndDate: "",
      inputStartDate: "",
      inputDescription: "",
      inputPlateform: "",
      inputType: "",
      inputProjectName: "",
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

    var apiURL = "http://localhost:8000/api/certificat/";

    fetch(apiURL + this.id, params)
      .then((response) => response.json())
      .then((data) => {
        this.certificatIdData = data;
        //console.log("apiurl + id + params", apiURL + this.id, params);
        //console.log("data", this.certificatIdData);
        const dataConnect = {
          projectName: (document.getElementById("projectName").value =
            this.certificatIdData.projectName),
          type: (document.getElementById("type").value =
            this.certificatIdData.type),
          plateform: (document.getElementById("plateform").value =
            this.certificatIdData.plateform),
          description: (document.getElementById("description").value =
            this.certificatIdData.description),
          startDate: (document.getElementById("startDate").value =
            this.certificatIdData.startDate),
          endDate: (document.getElementById("endDate").value =
            this.certificatIdData.endDate),
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
        projectName: document.getElementById("projectName").value,
        type: document.getElementById("type").value,
        plateform: document.getElementById("plateform").value,
        description: document.getElementById("description").value,
        startDate: document.getElementById("startDate").value,
        endDate: document.getElementById("endDate").value,
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

      var apiURL = "http://localhost:8000/api/certificat/";

      fetch(apiURL + this.id, params).then((response) => response.json());
      /* .then((data) => {
          this.certificatIdData = data;
        }); */
      console.log("apiurl + id + params", apiURL + this.id, params);
      //console.log("data", this.certificatIdData);
      this.$router.push("/certificats/");
    },
  },
};
</script>
