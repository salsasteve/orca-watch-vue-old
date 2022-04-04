<template>
  <div>
    <h2>{{ tokenPrice }}</h2>
    <hr />
    <small>Token ID: {{ $route.params.id }}</small>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      tokenPrice: {},
    };
  },
  async created() {
    const config = {
      headers: {
        Accept: "application/json",
      },
    };

    try {
      const res = await axios.get(
        `https://api.coingecko.com/api/v3/simple/price?ids=${this.$route.params.id}&vs_currencies=usd`,
        config
      );

      this.tokenPrice = res.data[this.$route.params.id].usd;
    } catch (err) {
      console.log(err);
    }
  },
  head() {
    return {
      title: this.$route.params.id,
      meta: [
        {
          hid: "description",
          name: "description",
          content: "Best place for corny dad jokes",
        },
      ],
    };
  },
};
</script>

<style></style>
