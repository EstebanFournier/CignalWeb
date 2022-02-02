<template>
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
    <div class="max-w-md w-34 space-y-8">
      <div>
        <img
          class="mx-auto h-20 w-auto"
          src="https://www.cubecom.fr/wp-content/uploads/2020/12/Logo-Cube-FondBlanc.png"
          alt=""
        />
      </div>
      <form class="mt-8 space-y-6" @submit.prevent="submit">
        <div class="shadow-sm -space-y-px">
          <input
            id="email-adress"
            name="email"
            type="text"
            v-model="inputEmail"
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
            placeholder="Adresse mail"
          />
        </div>
        <div class="shadow-sm -space-y-px">
          <input
            id="password"
            name="password"
            type="password"
            v-model="inputPassword"
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
            placeholder="Mot de passe"
          />
        </div>
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
            <span class="absolute left-0 inset-y-0 flex items-center pl-3">
              <svg
                class="h-5 w-5 text-white group-hover:text-white"
                xmlns="http://www.w3.org/2000/svg"
                viewBox="0 0 20 20"
                fill="currentColor"
                aria-hidden="true"
              >
                <path
                  fill-rule="evenodd"
                  d="M5 9V7a5 5 0 0110 0v2a2 2 0 012 2v5a2 2 0 01-2 2H5a2 2 0 01-2-2v-5a2 2 0 012-2zm8-2v2H7V7a3 3 0 016 0z"
                  clip-rule="evenodd"
                />
              </svg>
            </span>
            SE CONNECTER
          </button>
        </div>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  layout: "login",
  data() {
    return {
      inputEmail: "",
      inputPassword: "",
      token: "",
      userData: {},
    };
  },

  methods: {
    submit() {
      const dataConnect = {
        email: this.inputEmail,
        password: this.inputPassword,
      };
      //console.log("ok", dataConnect);

      var myInit = {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify(dataConnect),
      };
      //console.log('params', myInit)

      var apiURL = "http://localhost:8000/api/login";

      fetch(apiURL, myInit)
        .then((response) => response.json())
        .then((data) => {
          this.token = data.token;
          this.userData = data.user;

          localStorage.setItem("Authorization", data.token);
          localStorage.setItem("userData", JSON.stringify(this.userData));

          this.$router.push("/dashboard");
        });
    },
  },
};
</script>
