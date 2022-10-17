<template>
  <h1>Search Stickers</h1>

  <search @buscar="getStickers" />

  <loading v-show="loading" />

  <div class="row">
    <div v-for="sticker in stickers" 
    :key="sticker.id" 
    class="col-12 col-md-4 g-3"
    >
      <Card :gif="sticker" />
    </div>
  </div>
</template>

<script>
import Card from "../components/Card.vue";
import Search from "../components/Search.vue";
import Loading from "../components/Loading.vue";

import smal from "sweetalert2"

export default {
    data: () => ({
        stickers: [],
        loading: true
    }),
    created() {
        this.getStickers();
    },
    methods: {
        async getStickers(busqueda = "call of duty") {
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
              `https://api.giphy.com/v1/stickers/search?api_key=9RPnL2GJv0m6TPAuVPp1lJiFJKpLCkeR&q=${busqueda}`
              );
            const { data } = await res.json();
            this.stickers = data;

            this.loading = false;

        },
    },
    components: { Card, Search, Loading },
};
</script>

