<template>
  <div class="mx-auto bg-transparent h-28 w-full">
    <div class="flex flex-row flex-wrap gap-3 mt-3">
      <div class="flex-initial bg-transparent w-64 h-28">
        <NuxtLink :to="`/dashboard`">
        <img
          src="https://www.cubecom.fr/wp-content/uploads/2020/12/Logo-Cube-FondBlanc.png"
        />
        </NuxtLink>
      </div>
      <div class="flex-auto bg-transparent-500 w-10 h-28">
        <h1 class=""></h1>
      </div>
      <div
        class="flex-initial bg-white w-64 h-28 ml-5 border-solid border-[#797979] border-2"
      >
        <svg
          xmlns="http://www.w3.org/2000/svg"
          class="flex-initial zh-6 w-6"
          viewBox="0 0 20 20"
          fill="currentColor"
        >
          <path
            fill-rule="evenodd"
            d="M10 9a3 3 0 100-6 3 3 0 000 6zm-7 9a7 7 0 1114 0H3z"
            clip-rule="evenodd"
          />
        </svg>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      titlePage: "",
    };
  },
};
</script>

<style></style>
