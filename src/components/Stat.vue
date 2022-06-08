<template>
    <div class="stats shadow">
  
  <div class="stat">
    <div class="stat-title">Total Page Views</div>
    <div class="stat-value">{{count}}</div>
    <div class="stat-desc">21% more than last month</div>
  </div>
  
</div>
</template>

<script>
import axios from "axios";
export default {
  name: "Biens",
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
        this.posts = response.data.count;
        console.log(response.data.count)
      })
      .catch((e) => {
        this.errors.push(e);
      });
    console.log(this.posts);
  },
};
</script>