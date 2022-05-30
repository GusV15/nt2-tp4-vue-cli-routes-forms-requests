<template>
  <div>
    <h1>Requests</h1>
    <button class="btn btn-success my-3 mr-3" @click="getUsersByXHRpromise()">
      Get Users by XHR
    </button>
    <button class="btn btn-success my-3 mr-3" @click="getUsersByFetch()">
      Get Users by Fetch
    </button>
    <button class="btn btn-success my-3 mr-3" @click="getUsersByAxios()">
      Get Users by Axios
    </button>
    <table v-if="users.length" class="table table-dark">
      <tr>
        <th>ID</th>
        <th>Name</th>
        <th>Phone</th>
        <th>Email</th>
      </tr>
      <tr v-for="{ name, email, phone, id: key } in users" :key="key">
        <td>{{ key }}</td>
        <td>{{ name }}</td>
        <td>{{ phone }}</td>
        <td>{{ email }}</td>
      </tr>
    </table>
    <div
      v-else-if="!users.length && loading"
      class="alert alert-dark"
      role="alert"
    >
      Loading...
    </div>
    <div
      v-else-if="!users.length && error"
      class="alert alert-danger"
      role="alert"
    >
      {{ error }}
    </div>
    <div v-else-if="!users.length" class="alert alert-warning" role="alert">
      Users have not loaded.
    </div>
  </div>
</template>

<script>
export default {
  components: {},
  name: "peticiones-view",
  data() {
    return {
      url: "https://6292a6709d159855f08ce57b.mockapi.io/p1/tp4/users",
      users: [],
      loading: false,
      error: "",
    };
  },
  methods: {
    wrapperXHRpromise() {
      return new Promise((resolve, reject) => {
        const xhr = new XMLHttpRequest();
        xhr.open("get", this.url);

        xhr.addEventListener("load", () => {
          if (xhr.status == 200) {
            let respuesta = JSON.parse(xhr.response);
            resolve(respuesta);
          } else {
            console.error("ERROR XHR cb (status)", xhr.status);
            let error = {
              title: "ERROR XHR cb (status)",
              status: xhr.status,
            };
            reject(error);
          }
        });

        xhr.addEventListener("error", (e) => {
          console.error("ERROR XHR cb (ajax)", e);
          let error = {
            title: "ERROR XHR cb (ajax)",
            info: e,
          };
          reject(error);
        });

        xhr.send();
      });
    },
    async getUsersByXHRpromise() {
      this.users = [];
      try {
        this.loading = true;
        let respuesta = await this.wrapperXHRpromise();
        this.loading = false;
        this.users = respuesta;
      } catch (error) {
        this.loading = false;
        this.error = error;
        console.error("Error XHRpromise", error);
      }
    },
    async getUsersByFetch() {
      this.users = [];
      try {
        this.loading = true;
        const response = await fetch(this.url);
        const users = await response.json();
        this.loading = false;
        this.users = users;
      } catch (error) {
        this.loading = false;
        this.error = error;
        console.error("Error Fetch:", error);
      }
    },
    async getUsersByAxios() {
      this.users = [];
      try {
        this.loading = true;
        const { data } = await this.axios(this.url);
        this.loading = false;
        this.users = data;
      } catch (error) {
        this.loading = false;
        this.error = error;
        console.error("Error Axios:", error);
      }
    },
  },
  computed: {},
};
</script>

<style>
</style>