<template>
  <div class="container mt-5">
    <div class="card my-2">
      <div class="card-body">
        <h1>Detalle del articulo id: {{ $route.params.id }}</h1>
        <!-- {{ autor.name }} -->
        <!-- {{ article }}
        <hr />
        {{ article.title }}
        <hr />
        {{ article.title }} -->
        <h3 class="card-title">{{ article.title }}</h3>
        <p class="card-text">{{ article.body }}</p>
        <p class="small">{{ autor.name }}</p>
        <nuxt-link to="/articulo" class="btn btn-primary">Atras</nuxt-link>
      </div>
    </div>
  </div>
</template>
<script>
import axios from "axios";
// https://composition-api.nuxtjs.org/helpers/usecontext/
// import { onMounted, ref, watch, useContext } from "@nuxtjs/composition-api";
// import { useRoute } from "vue-router";
import { defineComponent, ref, useContext } from "@nuxtjs/composition-api";

// export default defineComponent({
//   setup() {
//     const { params } = useContext();
//     // console.log(params.value.id);
//     const id = params.value.id;
//     const article = ref({});
//     const getArticle = async () => {
//       console.log("getArticle");
//       try {
//         const result = await axios.get(
//           // `https://jsonplaceholder.typicode.com/users/${id}`
//           `https://jsonplaceholder.typicode.com/posts/${id}`
//         );
//         console.log(result.data);
//         article.value = await result.data;
//       } catch (error) {
//         console.log(error);
//       }
//     };
//     getArticle();

//     return { article };
//   },
// });

export default {
  setup() {
    //   const { params } = useContext();
    //   // console.log(params.value.id);
    //   const id = params.value.id;
    //   const article = ref({});
    //   const autor = ref({});
    //   const getArticle = async () => {
    //     console.log("getArticle");
    //     try {
    //       const result = await axios.get(
    //         // `https://jsonplaceholder.typicode.com/users/${id}`
    //         `https://jsonplaceholder.typicode.com/posts/${id}`
    //       );
    //       // console.log(result.data);
    //       article.value = await result.data;
    //       const autorId = article.value.userId;
    //       const autorRes = await axios.get(
    //         `https://jsonplaceholder.typicode.com/users/${autorId}`
    //       );
    //       autor.value = await autorRes.data;
    //     } catch (error) {
    //       console.log(error);
    //     }
    //   };
    //   getArticle();
    //   return { article, autor };
  },

  async asyncData({
    isDev,
    route,
    store,
    env,
    params,
    query,
    req,
    res,
    redirect,
    error,
  }) {
    const articleId = params.id;
    // console.log(params);
    try {
      const result = await axios.get(
        // `https://jsonplaceholder.typicode.com/users/${id}`
        `https://jsonplaceholder.typicode.com/posts/${articleId}`
      );
      // console.log(result.data);
      const article = await result.data;

      const autorId = article.userId;

      const autorRes = await axios.get(
        `https://jsonplaceholder.typicode.com/users/${autorId}`
      );
      const autor = await autorRes.data;
      return { article, autor };
    } catch (error) {
      console.log(error);
      return { error: error };
    }
  },
};
</script>
