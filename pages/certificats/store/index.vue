<template>
  <div>
    <TheHeader title="Enregistrer un nouveau certificat"></TheHeader>
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
            id="projectName"
            name="projectName"
            type="text"
            v-model="storeCertificat.projectName"
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
            placeholder="Nom du projet"
          />
        </div>
        <div class="shadow-sm -space-y-px">
          <input
            id="type"
            name="tsype"
            type="text"
            v-model="storeCertificat.type"
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
            placeholder="Type"
          />
        </div>
        <div class="shadow-sm -space-y-px">
          <input
            id="plateforme"
            name="plateforme"
            type="text"
            v-model="storeCertificat.plateform"
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
            placeholder="Plateforme"
          />
        </div>
        <div class="shadow-sm -space-y-px">
          <input
            id="description"
            name="description"
            type="text"
            v-model="storeCertificat.description"
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
            placeholder="Description"
          />
        </div>
        <div class="shadow-sm -space-y-px">
          <input
            id="startDate"
            name="startDate"
            type="date"
            v-model="storeCertificat.startDate"
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
            placeholder="Date de début"
          />
        </div>
        <div class="shadow-sm -space-y-px">
          <input
            id="endDate"
            name="endDate"
            type="date"
            v-model="storeCertificat.endDate"
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
            placeholder="Date de fin"
          />
        </div>
        <!-- <div class="shadow-sm -space-y-px">
          <input
            id="createdBy"
            name="createdBy"
            type="text"
            v-model="storeCertificat.createdBy"
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
            placeholder="Créé par"
          />
        </div>
        <div class="shadow-sm -space-y-px">
          <input
            id="email"
            name="email"
            type="email"
            v-model="storeCertificat.email"
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
            placeholder="Emai lié au certificat"
          />
        </div> -->
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
            Enregistrer le nouveau certificat
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
      storeCertificat: {
        projectName: "",
        type: "",
        plateform: "",
        description: "",
        startDate: "",
        endDate: "",
        /* createdBy: "",
        email: "", */
      },
    };
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
        body: JSON.stringify(this.storeCertificat),
      };

      var apiURL = "http://localhost:8000/api/certificat";

      fetch(apiURL, myInit)
        .then((response) => response.json())
        .catch((error) => {
          console.log("error", error);
        })
        .finally(() => {
          return this.$router.push("/certificats/");
        });
      console.log("params + apiURL", apiURL, myInit);
    },
  },
};
</script>
