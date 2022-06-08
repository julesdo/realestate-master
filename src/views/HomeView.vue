<template>
  <div class="home">
    <Hero/>
    <div>
    
    <h1 class="title text-xl font-bold text-left m-6">Nos biens</h1>
    <div class="carousel carousel-center w-full p-4 space-x-4 rounded-box">
        
        <Bien v-for="post in posts" :key="post.id" :Name="post.Name"
           :id="post.id" :image="post.image" :price="post.price" :category="post.category.value" :Notes="post.Notes">      
        </Bien>
        
    </div>
    
  </div>
    <Meteo/>
    <Hours/>
  </div>
</template>

<script>
// @ is an alias to /src
import Hero from "../components/Hero.vue"
import Meteo from "../components/Meteo.vue"
import Hours from "../components/Hours.vue"
import Bien from "../components/Bien.vue"
import axios from 'axios'
export default {
  name: 'HomeView',
  components: {
    Hero, Meteo, Hours, Bien
  },
  data() {
    return {
      posts: null,
      loading: false,
      errored: false,
    };
  },
  created() {
    axios
      .get(
        "https://api.baserow.io/api/database/rows/table/59933/?user_field_names=true",
        {
          headers: {
            Authorization: "Token X91rxzQ1mxHmUhaKoulQLdCrsHeKrkWq",
          },
        }
      )
      .then((response) => {
        this.posts = response.data.results;
        console.log(response.data.results);
      })
      .catch((e) => {
        this.errors.push(e);
      });
    console.log(this.posts);
  },
}
</script>
