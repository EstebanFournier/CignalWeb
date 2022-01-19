<template>
  <div>
    <TheHeader />
    <NavBar />
    <div class="mt-4" v-for="alert in alertData" :key="alert.id">
      <br />
      <h1>
        {{ alert.id }}
      </h1>
      <h2>
        {{ alert.projectName }}
      </h2>
      <p>
        {{ alert.description }}
      </p>
      <div>
        <NuxtLink :to="`/alerts/${alert.id}`">
          <svg
            xmlns="http://www.w3.org/2000/svg"
            class="h-5 w-5"
            viewBox="0 0 20 20"
            fill="currentColor"
          >
            <path d="M10 12a2 2 0 100-4 2 2 0 000 4z" />
            <path
              fill-rule="evenodd"
              d="M.458 10C1.732 5.943 5.522 3 10 3s8.268 2.943 9.542 7c-1.274 4.057-5.064 7-9.542 7S1.732 14.057.458 10zM14 10a4 4 0 11-8 0 4 4 0 018 0z"
              clip-rule="evenodd"
            />
          </svg>
        </NuxtLink>
      </div>
      <div>
        <NuxtLink :to="`/alerts/update/${alert.id}`">
          <svg
            xmlns="http://www.w3.org/2000/svg"
            class="h-6 w-6"
            fill="none"
            viewBox="0 0 24 24"
            stroke="currentColor"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M11 5H6a2 2 0 00-2 2v11a2 2 0 002 2h11a2 2 0 002-2v-5m-1.414-9.414a2 2 0 112.828 2.828L11.828 15H9v-2.828l8.586-8.586z"
            />
          </svg>
        </NuxtLink>
      </div>
      <div>
        <NuxtLink :to="`/alerts/delete/${alert.id}`">
          <svg
            xmlns="http://www.w3.org/2000/svg"
            class="h-6 w-6"
            fill="none"
            viewBox="0 0 24 24"
            stroke="currentColor"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M19 7l-.867 12.142A2 2 0 0116.138 21H7.862a2 2 0 01-1.995-1.858L5 7m5 4v6m4-6v6m1-10V4a1 1 0 00-1-1h-4a1 1 0 00-1 1v3M4 7h16"
            />
          </svg>
        </NuxtLink>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      alertData: "",
    };
  },

  async created() {
    let auth = localStorage.getItem("Authorization");
    console.log("auth", auth);

    var params = {
      method: "GET",
      headers: {
        "Content-Type": "application/json",
        Authorization: "Bearer " + auth,
      },
    };
    //console.log('params', params)

    var apiURL = "http://localhost:8000/api/alert/";
    //console.log('apiURL', apiURL)

    fetch(apiURL, params)
      .then((response) => response.json())
      .then((data) => {
        //console.log(data)
        this.alertData = data;
        //console.log("data", this.alertData);
      });
  },
};
</script>
