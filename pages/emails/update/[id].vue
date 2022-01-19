<template>
  <div>
    <TheHeader />
    <NavBar />
    <form id="form" method="PUT">
      <div>
        <input
          id="email"
          name="email"
          type="text"
          value="email"
          class=""
          placeholder="Email"
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
      emailIdData: "",
      id: "",
      inputEmail: "",
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

    var apiURL = "http://localhost:8000/api/email/";

    fetch(apiURL + this.id, params)
      .then((response) => response.json())
      .then((data) => {
        this.emailIdData = data;
        //console.log("apiurl + id + params", apiURL + this.id, params);
        //console.log("data", this.certificatIdData);
        const dataConnect = {
          email: (document.getElementById("email").value =
            this.emailIdData.email),
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
        email: document.getElementById("email").value,

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
