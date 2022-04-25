<template>
  <div class="float-left bg-transparent h-full w-64">
    <div class="flex-initial bg-transparent w-64 h-28">
      <NuxtLink :to="`/certificats`">
        <img
          src="https://www.cubecom.fr/wp-content/uploads/2020/12/Logo-Cube-FondBlanc.png"
        />
      </NuxtLink>
    </div>
    <div class="flex flex-col gap-3 mt-10 ml-5 mb-10">
      <NuxtLink :to="`/certificats/`" class="relative px-6 py-2 group">
        <span
          class="absolute inset-0 w-48 h-10 transition duration-300 ease-out transform translate-x-1 translate-y-1 bg-black group-hover:-translate-x-0 group-hover:-translate-y-0"
        ></span>
        <span
          class="absolute inset-0 w-48 h-10 bg-white border-2 border-black group-hover:bg-black"
        ></span>
        <span class="relative text-black group-hover:text-white">Certificats</span>
      </NuxtLink>
      <NuxtLink :to="`/alerts/`" class="relative px-6 py-2 group">
        <span
          class="absolute inset-0 w-48 h-10 transition duration-300 ease-out transform translate-x-1 translate-y-1 bg-black group-hover:-translate-x-0 group-hover:-translate-y-0"
        ></span>
        <span
          class="absolute inset-0 w-48 h-10 bg-white border-2 border-black group-hover:bg-black"
        ></span>
        <span class="relative text-black group-hover:text-white">Alertes</span>
      </NuxtLink>
      <NuxtLink :to="`/emails`" class="relative px-6 py-2 group">
        <span
          class="absolute inset-0 w-48 h-10 transition duration-300 ease-out transform translate-x-1 translate-y-1 bg-black group-hover:-translate-x-0 group-hover:-translate-y-0"
        ></span>
        <span
          class="absolute inset-0 w-48 h-10 bg-white border-2 border-black group-hover:bg-black"
        ></span>
        <span class="relative text-black group-hover:text-white">Emails</span>
      </NuxtLink>
      <NuxtLink :to="`/register`" class="relative px-6 py-2 group">
        <span
          class="absolute inset-0 w-48 h-10 transition duration-300 ease-out transform translate-x-1 translate-y-1 bg-black group-hover:-translate-x-0 group-hover:-translate-y-0"
        ></span>
        <span
          class="absolute inset-0 w-48 h-10 bg-white border-2 border-black group-hover:bg-black"
        ></span>
        <span class="relative text-black group-hover:text-white">Nouvel utilisateur</span>
      </NuxtLink>
      <button class="mt-96" @click="logout" type="submit">Déconnexion</button>
    </div>
  </div>
</template>

<script>
export default {
  /*
   Appel de la route logout
   */
  methods: {
    logout() {
      // Récupération du token d'authentification
      let auth = localStorage.getItem("Authorization");

      // Création des paramètres de la requête
      var params = {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
          Authorization: "Bearer " + auth,
        },
      };

      // URL de la reqête
      var apiURL = "http://192.168.200.156:8000/api/logout";

      // Execution de la requête et supression du token dans le cache client.
      fetch(apiURL, params).then((response) => response.json());
      if (localStorage && localStorage.length > 0) {
        localStorage.clear();
      }

      // Redirection vers la vue Login
      this.$router.push("/");
    },
  },
};
</script>

<style></style>
