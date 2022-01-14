<template>
  <!-- component -->
  <div class="bg-white shadow-md rounded px-8 pt-6 pb-8 mb-4 flex flex-col">
    <div class="mb-4">
      <input
        v-model="inputEmail"
        class="shadow appearance-none border rounded w-full py-2 px-3 text-grey-darker"
        id="username"
        type="text"
        placeholder="Adresse mail"
      />
    </div>
    <div class="mb-6">
      <input
        v-model="inputPassword"
        class="shadow appearance-none border border-red rounded w-full py-2 px-3 text-grey-darker mb-3"
        id="password"
        type="password"
        placeholder="Mot de passe"
      />
    </div>
    <div class="flex items-center justify-between">
      <button
        @click="submit"
        class="bg-blue hover:bg-blue-dark text-white font-bold py-2 px-4 rounded"
        type="button"
      >
        Se connecter
      </button>
    </div>
  </div>
</template>

<script>

export default {
  data (){
    return{
      inputEmail: "",
      inputPassword: "",
      token:"",
    }
  },

  methods:{
    submit() {
      const dataConnect = {
        'email': this.inputEmail,
        'password': this.inputPassword
      }
      //console.log('ok', dataConnect)

      var myInit = {
        method: "POST",
        headers: { "Content-Type": "application/json", },
        body: JSON.stringify(dataConnect)      
      }

      var apiURL = 'http://localhost:8000/api/login';

      fetch(apiURL, myInit)
      .then(response => response.json())
      .then(data => {
        //console.log('token', data)
        this.token = data.token
        console.log('token', data)

        localStorage.setItem('Authorization', data.token);
        console.log('localstorage', localStorage)

        /* var params = {
        method: "POST",
        headers: { "Content-Type": "application/json", "Authorization": data.token},
        body: JSON.stringify(dataConnect)      
        }
        console.log('params', params) */
      });
    }
  }
};
</script>