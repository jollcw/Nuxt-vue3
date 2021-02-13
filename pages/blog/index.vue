<template>
  <div class="container mt-5">
    <div class="row">
      <div class="col-md-3">
        <h1>blog</h1>
        <ul>
          <li v-for="(item, index) in articulos" :key="index">
            <nuxt-link :to="`/blog/${item.id}`">{{item.titulo}}</nuxt-link>
          </li>
        </ul>

      </div>
    </div>
  </div>
</template>
<script>
import { reactive, toRefs } from '@nuxtjs/composition-api'
export default {
  setup() {
    const data = reactive({
      articulos: [
        {id: 1, titulo: 'Articulo 1'},
        {id: 2, titulo: 'Articulo 2'},
        {id: 3, titulo: 'Articulo 3'},
        {id: 4, titulo: 'Articulo 4'}
      ]
    })
    return { ...toRefs(data)}
  }
}
</script>
