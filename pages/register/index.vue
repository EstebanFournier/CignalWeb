<template>
  <div>
    <TheHeader title="Enregistrer un nouvel utilisateur"></TheHeader>

    <div class="min-h-full flex items-center justify-center py-12 px-4 sm:px-6 lg:px-8">
      <form class="mt-8 space-y-6" id="form" method="PUT" @submit="submit">
        <div class="shadow-sm -space-y-px">
          <input
            id="email-adress"
            name="email"
            type="text"
            v-model="register.name"
            class="appearance relative block w-full px-3 py-2 border border-black placeholder-black-500 text-black focus:outline-none focus:ring-red-500 focus:border-red-500 focus:z-10 sm:text-sm"
            placeholder="Nom de l'utilisateur"
          />
        </div>
        <div class="shadow-sm -space-y-px">
          <input
            id="email-adress"
            name="email"
            type="email"
            v-model="register.email"
            class="appearance relative block w-full px-3 py-2 border border-black placeholder-black-500 text-black focus:outline-none focus:ring-red-500 focus:border-red-500 focus:z-10 sm:text-sm"
            placeholder="Adresse mail de l'utilisateur"
          />
        </div>
        <div class="shadow-sm -space-y-px">
          <input
            id="password"
            name="password"
            type="password"
            v-model="register.password"
            class="appearance relative block w-full px-3 py-2 border border-black placeholder-black-500 text-black focus:outline-none focus:ring-red-500 focus:border-red-500 focus:z-10 sm:text-sm"
            placeholder="Mot de passe de l'utilisateur"
          />
        </div>
        <div class="shadow-sm -space-y-px">
          <input
            id="password"
            name="password"
            type="password"
            v-model="register.password_confirmation"
            class="appearance relative block w-full px-3 py-2 border border-black placeholder-black-500 text-black focus:outline-none focus:ring-red-500 focus:border-red-500 focus:z-10 sm:text-sm"
            placeholder="Confirmer le mot de passe"
          />
        </div>
        <div>
          <button
            type="submit"
            class="group relative w-full flex justify-center py-2 px-4 border border-transparent text-sm font-medium text-white bg-red-600 hover:bg-red-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-red-500"
          >
            Enregistrer le nouvel utilisateur
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
      register: {
        name: "",
        email: "",
        password: "",
        password_confirmation: "",
      },
    };
  },

  // Récupération des données du nouvel utilisateur puis enregistrement de l'utilisateur
  methods: {
    submit(e) {
      e.preventDefault();

      console.log("registerdata", register);

      let auth = localStorage.getItem("Authorization");

      var myInit = {
        method: "PUT",
        headers: {
          "Content-Type": "application/json",
          Authorization: "Bearer " + auth,
        },
        body: JSON.stringify(this.register),
      };
      console.log("params", myInit);

      var apiURL = "http://192.168.200.156:8000/api/register";

      fetch(apiURL, myInit)
        .then((response) => response.json())
        .catch((error) => {
          console.log("error", error);
        })
        .finally(() => {
          return this.$router.push("/dashboard/");
        });
    },
  },
};
</script>
