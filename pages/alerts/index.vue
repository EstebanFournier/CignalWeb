<template>
  <div>
    <div class="mt-4" v-for="alert in alertData" :key="alert.id">
      <NuxtLink :to="`/alerts/${alert.id}`">
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
      </NuxtLink>
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
    console.log('auth', auth)

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
