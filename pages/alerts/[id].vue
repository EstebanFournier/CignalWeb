<template>
  <div>
    <TheHeader title="Alertes"></TheHeader>
    <div>
      <!-- light mode -->
      <div class="max-w-2xl mx-auto sm:px-6 lg:px-8">
        <div class="overflow-hidden shadow-md">
          <!-- card header -->
          <div class="px-6 py-4 bg-white border-b border-gray-200 font-bold uppercase">
            Alerte n° :
            {{ alertIdData.id }}
          </div>

          <!-- card body -->
          <div class="p-6 bg-white border-b border-gray-200">
            <!-- content goes here -->
            <p><strong> Nom de l'alerte : </strong>{{ alertIdData.nameAlert }}</p>
            <p>
              <strong> Description de l'alerte : </strong>{{ alertIdData.description }}
            </p>
            <p>
              <strong> ID du certificat lié : </strong>{{ alertIdData.certificat_id }}
            </p>
            <p><strong> Date de l'alerte : </strong>{{ alertIdData.dateAlert }}</p>
          </div>

          <!-- card footer -->
          <div class="p-6 bg-white border-gray-200 text-right">
            <!-- button link -->
            <NuxtLink
              :to="`/alerts`"
              class="bg-red-500 shadow-md text-sm text-white font-bold py-3 md:px-8 px-4 hover:bg-red-300 rounded uppercase"
              >Retour</NuxtLink
            >
          </div>
        </div>
      </div>
    </div>
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

  // Récupération des données par id
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

    var apiURL = "http://192.168.200.161:8000/api/alert/";

    fetch(apiURL + this.id, params)
      .then((response) => response.json())
      .then((response) => {
        this.alertIdData = response;
      })
      .catch((error) => {
        console.log("error", error);
      });
  },
};
</script>
