<template>
  <div>
    <TheHeader title="Enregistrer une nouvelle alerte"></TheHeader>
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
            id="dateAlert"
            name="dateAlert"
            type="date"
            v-model="storeAlert.dateAlert"
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
            placeholder="Date"
          />
        </div>
        <div class="shadow-sm -space-y-px">
          <input
            id="nameAlert"
            name="nameAlert"
            type="text"
            v-model="storeAlert.nameAlert"
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
          <input
            id="description"
            name="description"
            type="text"
            v-model="storeAlert.description"
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
            id="certificat_id"
            name="certificat_id"
            type="id"
            v-model="storeAlert.certificat_id"
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
            placeholder="Numéro du certificat"
          />
        </div>
        <!-- 
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
        <div class="shadow-sm -space-y-px">
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
      storeAlert: {
        dateAlert: "",
        nameAlert: "",
        certificat_id: "",
        description: "",
        /* startDate: "",
        endDate: "", */
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
        body: JSON.stringify(this.storeAlert),
      };

      var apiURL = "http://localhost:8000/api/alert";

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
