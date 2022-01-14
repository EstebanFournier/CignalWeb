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
  data () {
    return{
      alertData: "",
    }
  },

  async created() {

    let auth = localStorage.getItem('Authorization');

    var params = {
    method: "GET",
    headers: { "Content-Type": "application/json", "Authorization": auth},   
    }
    console.log('params', params)
     
    var apiURL = "http://localhost:8000/api/alert/";

    /*const response = await fetch(apiURL, params).then(
      (data) => data.json()
    );
    this.alertData = response; */
    
    fetch(apiURL, params)
      .then(response => response.json())
      .then(data => {
        this.alertData = response
      },)
  }
}
</script>