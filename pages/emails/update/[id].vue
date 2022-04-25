<template>
  <div>
    <TheHeader />
    <form id="form" method="PUT" @submit="submit">
      <div>
        <input
          id="email"
          name="email"
          type="text"
          v-model="emailIdData.email"
          class="appearance relative block w-48 px-3 py-2 border border-black placeholder-black-500 text-black focus:outline-none focus:ring-red-500 focus:border-red-500 focus:z-10 sm:text-sm"
          placeholder="Email"
        />
      </div>
      <div>
        <br />
        <button
          class="group relative w-48 flex justify-center py-2 px-4 border border-transparent text-sm font-medium text-white bg-red-600 hover:bg-red-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-red-500"
          type="submit"
        >
          Mettre à jour
        </button>
      </div>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      emailIdData: {
        email: "",
      },
      id: "",
    };
  },

  // Récupération des données avant update
  async mounted() {
    let auth = localStorage.getItem("Authorization");

    this.id = this.$route.params.id;

    var params = {
      method: "GET",
      headers: {
        "Content-Type": "application/json",
        Authorization: "Bearer " + auth,
      },
    };

    var apiURL = "http://192.168.200.156:8000/api/email/";

    fetch(apiURL + this.id, params)
      .then((response) => response.json())
      .then((response) => {
        this.emailIdData = response;
      })
      .catch((error) => {
        console.log("error", error);
      });
  },

  // Récupération des données pour update puis execution de l'update
  methods: {
    submit(e) {
      e.preventDefault();

      let auth = localStorage.getItem("Authorization");

      var params = {
        method: "PUT",
        headers: {
          "Content-Type": "application/json",
          Authorization: "Bearer " + auth,
        },
        body: JSON.stringify(this.emailIdData),
      };

      var apiURL = "http://192.168.200.156:8000/api/email/";

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
