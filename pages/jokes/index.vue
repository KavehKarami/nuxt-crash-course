<template>
  <div>
    <Joke v-for="joke of jokes" :id="joke.id" :key="joke.id" :joke="joke.joke" />
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "Jokes",

  data() {
    return {
      jokes: []
    }
  },
  
  head(){
    return {
      title: "dad jokes",
      meta: [
        {
          hid: "description",
          name: "description",
          content: "best place for corny dad jokes"
        }
      ]
    }
  },

  async mounted () {
    const config = {
      headers: {
        Accept: "application/json"
      }
    }

    try {
      const res = await axios.get("https://icanhazdadjoke.com/search", config);
      this.jokes = res.data.results;
    } catch (err) {
      throw new Error(err)
    }
  },
}
</script>

<style lang="scss" scoped>

</style>