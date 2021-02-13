<template>
  <div class="container mt-5">
    <h1>Blog</h1>
    <div class="card my-2" v-for="(art, index) in res" :key="index">
      <div class="card-body">
        <h2>{{ art.title }}</h2>
        <h3>{{ art.id }}</h3>
        <p>{{ art.body }}</p>
      </div>
    </div>
    <!-- {{res}} -->
  </div>
</template>
<script>
// import { reactive, toRefs, onMounted, ref } from '@nuxtjs/composition-api'
import { onMounted, ref } from "@nuxtjs/composition-api";
import axios from "axios";

export default {
  setup() {
    const res = ref(null);
    onMounted(async () => {
      const response = await axios.get(
        "https://jsonplaceholder.typicode.com/posts?_limit=10"
      );
      res.value = await response.data;
      // console.log('res.value', res.value);
    });
    //
    return { res };
  },
};
</script>
