<template>
  <div>
    <TheHeader title="Certificats"></TheHeader>
    <div class="">
      <!-- light mode -->
      <div class="max-w-2xl mx-auto sm:px-6 lg:px-8">
        <div class="overflow-hidden shadow-md">
          <!-- card header -->
          <div class="px-6 py-4 bg-white border-b border-gray-200 font-bold uppercase">
            Certificat n° :
            {{ certificatIdData.id }}
          </div>

          <!-- card body -->
          <div class="p-6 bg-white border-b border-gray-200">
            <!-- content goes here -->
            <p><strong> Nom du projet : </strong>{{ certificatIdData.projectName }}</p>
            <p>
              <strong> Description du projet : </strong>{{ certificatIdData.description }}
            </p>
            <p><strong> Type de certificat : </strong>{{ certificatIdData.type }}</p>
            <p><strong> Platforme concerné : </strong>{{ certificatIdData.plateform }}</p>
            <p><strong> Date de début : </strong>{{ certificatIdData.startDate }}</p>
            <p><strong> Date de fin :</strong>{{ certificatIdData.endDate }}</p>
          </div>

          <!-- card footer -->
          <div class="p-6 bg-white border-gray-200 text-right">
            <!-- button link -->
            <NuxtLink
              :to="`/certificats`"
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
      certificatIdData: "",
      id: "",
    };
  },

  // Récupération des données en fonction de l'id
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
      })
      .catch((error) => {
        console.log("error", error);
      });
  },
};
</script>
