<template>
  <h1 class="text-center">Gif Router</h1>
  <img :src="img" :alt="name" />
</template>

<script>
export default {
  data: () => ({
    img: "",
    name: "",
  }),
  created () {
    this.getRandomGif();
  },
  methods: {
    async getRandomGif() {
      const data = await fetch(
        "https://api.giphy.com/v1/gifs/random?api_key=9RPnL2GJv0m6TPAuVPp1lJiFJKpLCkeR"
      );
      const res = await data.json();

      this.img = res.data.images.original.url;
      this.name = res.data.title;

      console.log(res.data.title);

    },
  },
};
</script>

