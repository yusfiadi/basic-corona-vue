<template>
  <v-app>
    <v-card color="grey lighten-4" flat height="auto">
      <v-toolbar>
        <!-- <v-app-bar-nav-icon></v-app-bar-nav-icon> -->
        <!-- <v-img :src="require('@/assets/logo_dpkm.png')"></v-img> -->
        <img :src="require('@/assets/logo_dpkm.png')" height="40" />
        <v-toolbar-title></v-toolbar-title>
      </v-toolbar>
    </v-card>
    <v-container class="grey lighten-5">
      <v-card>
        <v-card-title>
          Data berdasarkan Provinsi
          <v-spacer></v-spacer>
          <v-text-field
            v-model="search"
            append-icon="mdi-magnify"
            label="Search"
            single-line
            hide-details
          ></v-text-field>
        </v-card-title>
        <v-data-table :headers="headers" :items="desserts" :search="search"></v-data-table>
      </v-card>
      <p class="float-left mt-5">
        *Data diperoleh dari
        <a href="https://kawalcorona.com/">kawalcorona.com</a>
      </p>
    </v-container>
  </v-app>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      search: "",
      // Data provinsi
      headers: [
        {
          text: "Provinsi",
          align: "start",
          value: "Provinsi"
        },
        { text: "Kasus Positif", value: "Kasus_Posi" },
        { text: "Kasus Sembuh", value: "Kasus_Semb" },
        { text: "Kasus Meninggal", value: "Kasus_Meni" }
      ],
      desserts: [],
      errors: []
    };
  },
  created() {
    axios
      .get("https://api.kawalcorona.com/indonesia/provinsi/") /* Data global */
      .then(response => {
        // console.log(response.data);
        for (let i = 0; i < response.data.length; i++) {
          this.desserts.push(response.data[i].attributes);
        }
      })
      .catch(e => {
        this.errors.push(e);
      });
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
</style>
