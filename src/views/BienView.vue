<template>
  <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
    <div class="content">
      <img :src="post.image" alt="" />
    </div>
    <div class="grid gap-2 card bg-base-100 rounded-none">
      <div class="card-body">
        <h2 class="card-title">{{ post.Name }}</h2>
        <div class="flex flex-wrap gap-2">
          <div class="badge badge-primary">$ {{ post.price }}</div>
          <div class="badge badge-secondary">{{ post.category.value }}</div>
          <div class="badge badge-accent">{{ post.adresse }}</div>
        </div>
        <p>{{ post.Notes }}</p>
        <a
          target="blank"
          :href="`https://www.google.fr/maps/place/${post.adresse}`"
          class="btn btn-secondary"
          >Google Map</a
        >
        <button @click="getAgent" class="btn btn-primary">
          Contacter l'agent immobilier
        </button>
        <div v-if="done===true" class="card card-side bg-base-100 shadow-xl">
          <figure>
            <img :src="agent.Image" alt="agent" />
          </figure>
          <div class="card-body">
            <h2 class="card-title">Gestionnaire de ce bien</h2>
            <h2 class="card-title">{{ agent.Name }} {{ agent.Firstname }}</h2>
            <div class="card-actions">
              <div class="flex flex-wrap gap-2">
                <p>Autres bien en gestion :</p>
                <div v-for="biens in agent.Biens" :key="biens">
                  <a
                  :href="link + biens.id"
                    class="badge badge-primary hover:badge-secondary cursor-pointer"
                    >{{ biens.value }}</a
                  >
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { useRoute } from "vue-router";
import axios from "axios";

export default {
  name: "bien",
  data() {
    return {
      agent: [],
      post: [],
      done:[],
      link: "/#/bien/",
    };
  },
  async created() {
    let id = parseInt(useRoute().params.id);
    axios
      .get(
        `https://api.baserow.io/api/database/rows/table/59933/${id}/?user_field_names=true`,
        {
          headers: {
            Authorization: "Token X91rxzQ1mxHmUhaKoulQLdCrsHeKrkWq",
          },
        }
      )
      .then((response) => {
        this.post = response.data;
        console.log(response.data.results);
      })
      .catch((e) => {
        this.errors.push(e);
      });
    console.log(post);
    getAgent();
  },
  methods: {
    async getAgent() {
      let agentId = this.post.Agent[0].id;
      console.log(agentId);
      axios
        .get(
          `https://api.baserow.io/api/database/rows/table/59958/${agentId}/?user_field_names=true`,
          {
            headers: {
              Authorization: "Token X91rxzQ1mxHmUhaKoulQLdCrsHeKrkWq",
            },
          }
        )
        .then((response) => {
          this.agent = response.data;
          console.log(response.data.results);
        })
        .catch((e) => {
          this.errors.push(e);
        });
      console.log(this.agent);
      this.done= true;
    },
  },
};
</script>

<style scoped></style>
