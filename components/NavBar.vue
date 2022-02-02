<template>
  <div class="float-left bg-transparent h-full w-64">
    <div class="flex-initial bg-transparent w-64 h-28">
      <NuxtLink :to="`/dashboard`">
        <img
          src="https://www.cubecom.fr/wp-content/uploads/2020/12/Logo-Cube-FondBlanc.png"
        />
      </NuxtLink>
    </div>
    <div class="flex flex-col gap-3 mt-10 ml-5 mb-10">
      <NuxtLink :to="`/dashboard`" class="relative px-6 py-2 group">
        <span
          class="
            absolute
            inset-0
            w-48
            h-10
            transition
            duration-300
            ease-out
            transform
            translate-x-1 translate-y-1
            bg-black
            group-hover:-translate-x-0 group-hover:-translate-y-0
          "
        ></span>
        <span
          class="
            absolute
            inset-0
            w-48
            h-10
            bg-white
            border-2 border-black
            group-hover:bg-black
          "
        ></span>
        <span class="relative text-black group-hover:text-white">Accueil</span>
      </NuxtLink>
      <NuxtLink :to="`/certificats/`" class="relative px-6 py-2 group">
        <span
          class="
            absolute
            inset-0
            w-48
            h-10
            transition
            duration-300
            ease-out
            transform
            translate-x-1 translate-y-1
            bg-black
            group-hover:-translate-x-0 group-hover:-translate-y-0
          "
        ></span>
        <span
          class="
            absolute
            inset-0
            w-48
            h-10
            bg-white
            border-2 border-black
            group-hover:bg-black
          "
        ></span>
        <span class="relative text-black group-hover:text-white"
          >Certificats</span
        >
      </NuxtLink>
      <NuxtLink :to="`/alerts/`" class="relative px-6 py-2 group">
        <span
          class="
            absolute
            inset-0
            w-48
            h-10
            transition
            duration-300
            ease-out
            transform
            translate-x-1 translate-y-1
            bg-black
            group-hover:-translate-x-0 group-hover:-translate-y-0
          "
        ></span>
        <span
          class="
            absolute
            inset-0
            w-48
            h-10
            bg-white
            border-2 border-black
            group-hover:bg-black
          "
        ></span>
        <span class="relative text-black group-hover:text-white">Alertes</span>
      </NuxtLink>
      <NuxtLink :to="`/emails`" class="relative px-6 py-2 group">
        <span
          class="
            absolute
            inset-0
            w-48
            h-10
            transition
            duration-300
            ease-out
            transform
            translate-x-1 translate-y-1
            bg-black
            group-hover:-translate-x-0 group-hover:-translate-y-0
          "
        ></span>
        <span
          class="
            absolute
            inset-0
            w-48
            h-10
            bg-white
            border-2 border-black
            group-hover:bg-black
          "
        ></span>
        <span class="relative text-black group-hover:text-white">Emails</span>
      </NuxtLink>
      <NuxtLink :to="`/emails`" class="relative px-6 py-2 group">
        <span
          class="
            absolute
            inset-0
            w-48
            h-10
            transition
            duration-300
            ease-out
            transform
            translate-x-1 translate-y-1
            bg-black
            group-hover:-translate-x-0 group-hover:-translate-y-0
          "
        ></span>
        <span
          class="
            absolute
            inset-0
            w-48
            h-10
            bg-white
            border-2 border-black
            group-hover:bg-black
          "
        ></span>
        <span class="relative text-black group-hover:text-white">Logs</span>
      </NuxtLink>
      <button @click="logout" type="submit">Logout</button>
      <NuxtLink :to="`/register`">Register</NuxtLink>
    </div>
  </div>
</template>

<script>
export default {
  methods: {
    logout() {
      let auth = localStorage.getItem("Authorization");
      //console.log("auth", auth);

      var params = {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
          Authorization: "Bearer " + auth,
        },
      };

      var apiURL = "http://localhost:8000/api/logout";

      fetch(apiURL, params).then((response) => response.json());
      if (localStorage && localStorage.length > 0) {
        localStorage.clear();
      }

      this.$router.push("/");
    },
  },
};
</script>

<style></style>
