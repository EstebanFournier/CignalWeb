<template>
  <div>
    <TheHeader title="Enregistrer un nouvel email"></TheHeader>
    <div
      class="
        min-h-full
        flex
        items-center
        justify-center
        py-12
        px-4
        sm:px-6
        lg:px-8
      "
    >
      <form class="mt-8 space-y-6" id="form" @submit.prevent="submit">
        <div class="shadow-sm -space-y-px">
          <input
            id="email"
            name="email"
            type="email"
            v-model="storeEmail.email"
            class="
              appearance
              relative
              block
              w-full
              px-3
              py-2
              border border-black
              placeholder-black-500
              text-black
              focus:outline-none
              focus:ring-red-500
              focus:border-red-500
              focus:z-10
              sm:text-sm
            "
            placeholder="Email"
          />
        </div>
        <div class="shadow-sm -space-y-px">
          <input
            id="name"
            name="name"
            type="text"
            v-model="storeEmail.name"
            class="
              appearance
              relative
              block
              w-full
              px-3
              py-2
              border border-black
              placeholder-black-500
              text-black
              focus:outline-none
              focus:ring-red-500
              focus:border-red-500
              focus:z-10
              sm:text-sm
            "
            placeholder="Nom"
          />
        </div>
        <div class="shadow-sm -space-y-px">
          <select
            v-model="storeEmail.user_id"
            class="
              appearance
              relative
              block
              w-full
              px-3
              py-2
              border border-black
              placeholder-black-500
              text-black
              focus:outline-none
              focus:ring-red-500
              focus:border-red-500
              focus:z-10
              sm:text-sm
            "
          >
            <option
              v-for="name in user_idChoose"
              :key="name.id"
              :value="name.id"
            >
              {{ name.id + " " + name.name }}
            </option>
          </select>
        </div>
        <div>
          <button
            type="submit"
            class="
              group
              relative
              w-full
              flex
              justify-center
              py-2
              px-4
              border border-transparent
              text-sm
              font-medium
              text-white
              bg-red-600
              hover:bg-red-700
              focus:outline-none
              focus:ring-2
              focus:ring-offset-2
              focus:ring-red-500
            "
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
      user_idChoose: [],
      storeEmail: {
        email: "",
        name: "",
        user_id: "",
      },
    };
  },

  async mounted() {
    let auth = localStorage.getItem("Authorization");

    var params = {
      method: "GET",
      headers: {
        "Content-Type": "application/json",
        Authorization: "Bearer " + auth,
      },
    };

    var apiURL = "http://localhost:8000/api/createdBy";

    fetch(apiURL, params)
      .then((response) => response.json())
      .then((response) => {
        this.user_idChoose = response;
        this.storeCertificat.user_id = this.user_idChoose[0].id;
        console.log("createdByChoose", this.user_idChoose);
      })
      .catch((error) => {
        console.log("error", error);
      });
  },

  methods: {
    submit() {
      let auth = localStorage.getItem("Authorization");

      var myInit = {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
          Authorization: "Bearer " + auth,
        },
        body: JSON.stringify(this.storeEmail),
      };

      var apiURL = "http://localhost:8000/api/email";

      fetch(apiURL, myInit)
        .then((response) => response.json())
        .catch((error) => {
          console.log("error", error);
        })
        .finally(() => {
          return this.$router.push("/emails/");
        });
      console.log("params + apiURL", apiURL, myInit);
    },
  },
};
</script>
