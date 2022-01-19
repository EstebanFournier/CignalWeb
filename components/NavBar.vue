<template>
  <div class="bg-transparent h-full w-64">
    <div class="flex flex-col gap-3 mt-10 ml-5 mb-10">
      <NuxtLink :to="`/`">
        <div
          class="flex-initial bg-transparent w-48 h-10 border-solid border-[#797979] border-2"
        >
          Accueil
        </div>
      </NuxtLink>
      <NuxtLink :to="`/certificats/`">
        <div
          class="flex-initial bg-transparent w-48 h-10 border-solid border-[#797979] border-2"
        >
          Certificats
        </div>
      </NuxtLink>
      <NuxtLink :to="`/alerts/`">
        <div
          class="flex-initial bg-transparent w-48 h-10 border-solid border-[#797979] border-2"
        >
          Alertes
        </div>
      </NuxtLink>
      <NuxtLink :to="`/emails`">
        <div
          class="flex-initial bg-transparent w-48 h-10 border-solid border-[#797979] border-2"
        >
          Emails
        </div>
      </NuxtLink>
      <NuxtLink :to="`/emails`">
        <div
          class="flex-initial bg-transparent w-48 h-10 border-solid border-[#797979] border-2"
        >
          Logs
        </div>
      </NuxtLink>
      <button @click="submit" type="submit">Logout</button>
    </div>
  </div>
</template>

<script>
export default {
  methods: {
    submit() {
      let auth = localStorage.getItem("Authorization");
      console.log("auth", auth);
      localStorage.clear.Authorization;
      console.log("storage", localStorage);

      var params = {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
          Authorization: "Bearer " + auth,
        },
      };

      var apiURL = "http://localhost:8000/api/logout";

      fetch(apiURL, params).then((response) => response.json());

      this.$router.push("/authenticate/login");
    },
  },
};
</script>

<style></style>
