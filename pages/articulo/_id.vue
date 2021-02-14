<template>
  <div class="container">
    <div class="card">
      <div class="body-card">
        <h1>Detalle del articulo id: {{ $route.params.id }}</h1>
        <!-- <h1>{{ article.title }}</h1>
        <p class="small">{{ article.userId }}</p>
        <p>{{ article.body }}</p> -->
        <nuxt-link to="/articulo" class="btn btn-primary">Atras</nuxt-link>
      </div>
    </div>
  </div>
</template>
<script>
import axios from "axios";
// https://composition-api.nuxtjs.org/helpers/usecontext/
import { onMounted, ref, watch, useContext } from "@nuxtjs/composition-api";
// import { useRoute } from "vue-router";

export default {
  setup() {
    const { params } = useContext();
    console.log(params.value.id);
    const id = params.value.id;

    const article = ref(null);
    const getArticle = async () => {
      console.log("getArticle");
      try {
        const result = await axios.get(
          `https://jsonplaceholder.typicode.com/users/${id}`
        );
        console.log(result.data);
        article.value = await result.data;
      } catch (error) {}
    };
    getArticle();
    return { article };
  },
};
</script>
