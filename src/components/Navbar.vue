<template>
<div class="navbar bg-base-100">
  <div class="flex-1">
    <router-link to="/">
      <a class="btn btn-ghost normal-case text-xl">daisyUI</a>
    </router-link>
    <div class="flex flex-row items-center gap-2">
      <img class="h-8" :src="posts.icon_big" alt="Shoes" />
      <p>{{ posts.tmp }} °C</p>
      <p>{{ location.name }}</p>
    </div>
  </div>
  <div class="flex-none">
    <ul class="menu menu-horizontal p-0">
      <router-link to="/bien"> 
      <li><a>Nos biens</a></li>
      </router-link>
    </ul>
  </div>
</div>

</template>

<script>
import axios from 'axios'
export default {
  name: "Navbar",
  data() {
    return {
      posts: [],
      loading: false,
      errored: false,
      location: [],
    };
  },
  created() {
    axios
      .get(
        "https://prevision-meteo.ch/services/json/artigues-pres-bordeaux")
      .then((response) => {
        console.log(response);
        this.posts = response.data.current_condition
        this.location = response.data.city_info
      })
      .catch((e) => {
        this.errors.push(e);
      });
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
