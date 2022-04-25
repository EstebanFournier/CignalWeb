<template>
  <div class="mx-auto bg-transparent h-28 w-full">
    <div class="flex flex-row flex-wrap gap-3 mt-3">
      <div class="flex-auto bg-transparent-500 w-10 h-28">
        <h1 class="uppercase font-bold text-4xl flex justify-center">{{ title }}</h1>
      </div>
      <div
        class="flex-initial bg-white w-64 h-28 ml-5 border-solid border-[#797979] border-2"
      >
        <h1 class="text-base">{{ dataUser.name }}</h1>
        <h1 class="text-sm italic">{{ dataUser.email }}</h1>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      dataUser: {},
    };
  },
  props: {
    title: {
      type: String,
      default: "Mon titre",
    },
  },
  async mounted() {
    // Récupération des données de l'utilisateur connecté
    this.dataUser = JSON.parse(localStorage.getItem("userData"));
  },
};
</script>

<style></style>
