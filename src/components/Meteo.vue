<template>
  <div class="card w-96 h-42 p-2 bg-base-100 shadow-xl flex flex-row">
      <figure><img :src="posts.icon_big" alt="Shoes" /></figure>
  <div class="card-body">
    <h2 class="text-2xl">{{posts.condition}}</h2>
    <p>{{ location.name }}</p>
    <div class="card-actions justify-center">
      <button class="btn btn-primary text-white">{{posts.tmp}} °C</button>
    </div>
  </div>
</div>
</template>

<script>
import axios from "axios";
export default {
  name: "Biens",
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
<style scoped></style>
