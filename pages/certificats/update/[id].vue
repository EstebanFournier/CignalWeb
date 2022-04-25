<template>
  <div>
    <TheHeader title="Certificats"></TheHeader>
    <form id="form" method="PUT" @submit="submit">
      <div>
        <input
          id="projectName"
          name="projectName"
          type="text"
          v-model="certificatIdData.projectName"
          class="mb-3 appearance relative block w-48 px-3 py-2 border border-black placeholder-black-500 text-black focus:outline-none focus:ring-red-500 focus:border-red-500 focus:z-10 sm:text-sm"
          placeholder="Nom du certificat"
        />
      </div>
      <div>
        <input
          id="type"
          name="type"
          type="text"
          v-model="certificatIdData.type"
          class="mb-3 appearance relative block w-48 px-3 py-2 border border-black placeholder-black-500 text-black focus:outline-none focus:ring-red-500 focus:border-red-500 focus:z-10 sm:text-sm"
          placeholder="Type de certificat"
        />
      </div>
      <div>
        <input
          id="plateform"
          name="plateform"
          type="text"
          v-model="certificatIdData.plateform"
          class="mb-3 appearance relative block w-48 px-3 py-2 border border-black placeholder-black-500 text-black focus:outline-none focus:ring-red-500 focus:border-red-500 focus:z-10 sm:text-sm"
          placeholder="Nom de la plateforme"
        />
      </div>
      <div>
        <input
          id="description"
          name="description"
          type="text"
          v-model="certificatIdData.description"
          class="mb-3 appearance relative block w-48 px-3 py-2 border border-black placeholder-black-500 text-black focus:outline-none focus:ring-red-500 focus:border-red-500 focus:z-10 sm:text-sm"
          placeholder="Description"
        />
      </div>
      <div>
        <input
          id="startDate"
          name="startDate"
          type="date"
          v-model="certificatIdData.startDate"
          class="mb-3 appearance relative block w-48 px-3 py-2 border border-black placeholder-black-500 text-black focus:outline-none focus:ring-red-500 focus:border-red-500 focus:z-10 sm:text-sm"
          placeholder="Date de début"
        />
      </div>
      <div>
        <input
          id="endDate"
          name="endDate"
          type="date"
          v-model="certificatIdData.endDate"
          class="appearance relative block w-48 px-3 py-2 border border-black placeholder-black-500 text-black focus:outline-none focus:ring-red-500 focus:border-red-500 focus:z-10 sm:text-sm"
          placeholder="Date de fin"
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
      certificatIdData: {
        projectName: "",
        type: "",
        plateform: "",
        description: "",
        startDate: "",
        endDate: "",
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

    var apiURL = "http://192.168.200.161:8000/api/certificat/";

    fetch(apiURL + this.id, params)
      .then((response) => response.json())
      .then((response) => {
        this.certificatIdData = response;
      });
  },

  // Récupération des données pour update et execution de l'update
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
        body: JSON.stringify(this.certificatIdData),
      };

      var apiURL = "http://192.168.200.156:8000/api/certificat/";

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
