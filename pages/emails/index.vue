<template>
  <div>
    <TheHeader title="Emails"></TheHeader>
    <div class="flex flex-col">
      <div class="-my-2 overflow-x-auto sm:-mx-6 lg:-mx-8">
        <div class="py-2 align-middle inline-block min-w-full sm:px-6 lg:px-8">
          <NuxtLink
            :to="`/emails/store/`"
            class="group relative w-48 flex justify-center py-2 px-4 border border-transparent text-sm font-medium text-white bg-red-600 hover:bg-red-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-red-500"
          >
            Ajouter un email
          </NuxtLink>
          <div class="shadow overflow-hidden border-b border-gray-200 sm:rounded-lg">
            <table class="min-w-full divide-y divide-gray-200">
              <thead class="bg-gray-50">
                <tr>
                  <th
                    class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider"
                  >
                    Numéro
                  </th>
                  <th
                    class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider"
                  >
                    Email
                  </th>
                  <th
                    class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider"
                  >
                    Nom
                  </th>
                  <th
                    class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider"
                  >
                    Actions
                  </th>
                </tr>
              </thead>
              <tbody class="bg-white divide-y divide-gray-200">
                <tr class="" v-for="email in emailData" :key="email.id">
                  <td class="px-8 py-4 whitespace-nowrap">
                    {{ email.id }}
                  </td>
                  <td class="px-8 py-4 whitespace-nowrap">
                    {{ email.email }}
                  </td>
                  <td class="px-8 py-4 whitespace-nowrap">
                    {{ email.name }}
                  </td>
                  <td
                    class="text-sm font-medium leading-5 text-center whitespace-no-wrap border-b border-gray-200"
                  >
                    <NuxtLink
                      :to="`/emails/update/${email.id}`"
                      class="text-indigo-600 hover:text-indigo-900"
                    >
                      <svg
                        xmlns="http://www.w3.org/2000/svg"
                        class="w-6 h-6"
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
                  </td>

                  <td
                    class="text-sm font-medium leading-5 whitespace-no-wrap border-b border-gray-200"
                  >
                    <NuxtLink :to="`/emails/delete/${email.id}`"
                      ><svg
                        xmlns="http://www.w3.org/2000/svg"
                        class="w-6 h-6 text-red-600 hover:text-red-800"
                        fill="none"
                        viewBox="0 0 24 24"
                        stroke="currentColor"
                      >
                        <path
                          stroke-linecap="round"
                          stroke-linejoin="round"
                          stroke-width="2"
                          d="M19 7l-.867 12.142A2 2 0 0116.138 21H7.862a2 2 0 01-1.995-1.858L5 7m5 4v6m4-6v6m1-10V4a1 1 0 00-1-1h-4a1 1 0 00-1 1v3M4 7h16"
                        /></svg
                    ></NuxtLink>
                  </td>
                </tr>
              </tbody>
            </table>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      emailData: "",
    };
  },

  // Récupération de toutes les données de la table Email
  async mounted() {
    let auth = localStorage.getItem("Authorization");

    var params = {
      method: "GET",
      headers: {
        "Content-Type": "application/json",
        Authorization: "Bearer " + auth,
      },
    };

    var apiURL = "http://192.168.200.156:8000/api/email";

    fetch(apiURL, params)
      .then((response) => response.json())
      .then((response) => {
        this.emailData = response;
      });
  },
};
</script>
