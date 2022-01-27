<template>
  <div>
    <TheHeader />
    <NavBar />
    <form id="form" method="PUT" @submit="submit">
      <div>
        <input
          id="email"
          name="email"
          type="text"
          v-model="emailIdData.email"
          class=""
          placeholder="Email"
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
      emailIdData: "",
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

    var apiURL = "http://localhost:8000/api/email/";

    fetch(apiURL + this.id, params)
      .then((response) => {
        this.emailIdData = response.json();
        //console.log("apiurl + id + params", apiURL + this.id, params);
        //console.log("data", this.certificatIdData);
      })
      .catch((error) => {
        console.log("error", error);
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
        body: JSON.stringify(this.emailIdData),
      };
      //console.log("params", params);

      var apiURL = "http://localhost:8000/api/email/";

      fetch(apiURL + this.id, params)
        .then((response) => response.json())
        .catch((error) => {
          console.log("error", error);
        })
        .finally(() => {
          this.$router.push("/emails/");
        });
      console.log("apiurl + id + params", apiURL + this.id, params);
    },
  },
};
</script>
