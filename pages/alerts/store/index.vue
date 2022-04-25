<template>
  <div>
    <TheHeader title="Enregistrer une nouvelle alerte"></TheHeader>
    <div class="min-h-full flex items-center justify-center py-12 px-4 sm:px-6 lg:px-8">
      <form class="mt-8 space-y-6" id="form" @submit.prevent="submit">
        <div class="shadow-sm -space-y-px">
          <input
            id="dateAlert"
            name="dateAlert"
            type="date"
            v-model="storeAlert.dateAlert"
            class="appearance relative block w-full px-3 py-2 border border-black placeholder-black-500 text-black focus:outline-none focus:ring-red-500 focus:border-red-500 focus:z-10 sm:text-sm"
            placeholder="Date"
          />
        </div>
        <div class="shadow-sm -space-y-px">
          <input
            id="nameAlert"
            name="nameAlert"
            type="text"
            v-model="storeAlert.nameAlert"
            class="appearance relative block w-full px-3 py-2 border border-black placeholder-black-500 text-black focus:outline-none focus:ring-red-500 focus:border-red-500 focus:z-10 sm:text-sm"
            placeholder="Nom"
          />
        </div>
        <div class="shadow-sm -space-y-px">
          <input
            id="description"
            name="description"
            type="text"
            v-model="storeAlert.description"
            class="appearance relative block w-full px-3 py-2 border border-black placeholder-black-500 text-black focus:outline-none focus:ring-red-500 focus:border-red-500 focus:z-10 sm:text-sm"
            placeholder="Description"
          />
        </div>

        <div class="shadow-sm -space-y-px">
          <select
            v-model="storeAlert.certificat_id"
            class="appearance relative block w-full px-3 py-2 border border-black placeholder-black-500 text-black focus:outline-none focus:ring-red-500 focus:border-red-500 focus:z-10 sm:text-sm"
          >
            <option v-for="name in certificat_idChoose" :key="name.id" :value="name.id">
              {{ name.id + " " + name.projectName }}
            </option>
          </select>
        </div>
        <div>
          <button
            type="submit"
            class="group relative w-full flex justify-center py-2 px-4 border border-transparent text-sm font-medium text-white bg-red-600 hover:bg-red-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-red-500"
          >
            Enregistrer une nouvelle alerte
          </button>
        </div>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      certificat_idChoose: [],
      storeAlert: {
        dateAlert: "",
        nameAlert: "",
        description: "",
        certificat_id: "",
      },
    };
  },

  // Récupération des données avant avant enregistrement
  async mounted() {
    let auth = localStorage.getItem("Authorization");

    var params = {
      method: "GET",
      headers: {
        "Content-Type": "application/json",
        Authorization: "Bearer " + auth,
      },
    };

    var apiURL = "http://192.168.200.161:8000/api/certificat";

    fetch(apiURL, params)
      .then((response) => response.json())
      .then((response) => {
        this.certificat_idChoose = response;
        this.storeAlert.certificat_id = this.certificat_idChoose[0].id;
        console.log("createdByChoose", this.certificat_idChoose);
      })
      .catch((error) => {
        console.log("error", error);
      });
  },

  // Récupération des données pour l'enregistrement et exceution de l'enregistrement
  methods: {
    submit() {
      let auth = localStorage.getItem("Authorization");

      var myInit = {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
          Authorization: "Bearer " + auth,
        },
        body: JSON.stringify(this.storeAlert),
      };

      var apiURL = "http://192.168.200.161:8000/api/alert";

      fetch(apiURL, myInit)
        .then((response) => response.json())
        .catch((error) => {
          console.log("error", error);
        })
        .finally(() => {
          return this.$router.push("/alerts/");
        });
      console.log("params + apiURL", apiURL, myInit);
    },
  },
};
</script>
