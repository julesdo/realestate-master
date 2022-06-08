<template>
      <router-link :to="{ name: 'bien', params: { id: id }}" class="container-movie">
        <div class="card w-96 bg-base-100 shadow-xl">
          <figure><img class="h-64" :src="image" alt="Shoes" /></figure>
          <div class="card-body">
            <h2 class="card-title">{{ Name }}</h2>
            <div class="flex flex-wrap gap-2">
              <div class="badge badge-primary">$ {{ price }}</div>
              <div class="badge badge-secondary">{{ category }}</div>
            </div>
            <p>{{ Notes }}</p>
          </div>
        </div>
      </router-link>
</template>

<script setup>

defineProps({
    id : Number,
    Name: String,
    image: String,
    price: String,
    category: String,
    Notes: String,
    Firstname: String,
    Image: String,
    score: String,
});
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
p {
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
  max-width: 10000px;
}
</style>