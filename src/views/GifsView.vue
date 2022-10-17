<template>
  <h1>Search Gif</h1>

  <search @buscar="getGifs" />

  <loading v-show="loading"/>

  <div class="row">
    <div v-for="gif in gifs" :key="gif.id" class="col-12 col-md-4 g-3">
  <Card :gif="gif" />
    </div>
  </div>
</template>

<script>
import Card from "../components/Card.vue";
import Search from "../components/Search.vue";
import Loading from "../components/Loading.vue";
import smal from 'sweetalert2';

export default {
    data: () => ({
        gifs: [],
        loading: true
    }),
    created() {
        this.getGifs();
    },
    methods: {
        async getGifs(busqueda = "star war jedi") {
          if (busqueda.trim() == "") {
            smal.fire({
              title: "Sem Busca",
              icon: "error",
              showConfirmButton: false,
              showCloseButton: true,
              timer: 3000,
              timerProgressBar: true,
            });
            return;
          }

          this.loading = true;

            const res = await fetch(
              `https://api.giphy.com/v1/gifs/search?api_key=9RPnL2GJv0m6TPAuVPp1lJiFJKpLCkeR&q=${busqueda}`
              );
            const { data } = await res.json();
            this.gifs = data;

            this.loading = false;
        },
    },
    components: { Card, Search, Loading },
};
</script>

