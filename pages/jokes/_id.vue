<template>
  <div>
    <h1 class="text-2xl mb-3 font-bold">jokeID : {{$route.params.id}}</h1>
    <p>{{joke.joke}}</p>
  </div>
</template>

<script>
export default {
  name: "SingleJokes",

  async asyncData ({ $axios , params }) {
    const config = {
      headers: {
        Accept: "application/json"
      }
    }
    const joke = await $axios.$get(`https://icanhazdadjoke.com/j/${params.id}`,config);
    return { joke }
  },

  data() {
    return {
      joke: {}
    }
  },

  head(){
    return {
      title: `jokeID : ${this.$route.params.id}`,
      meta: [
        {
          hid: "description",
          name: "description",
          content: "best place for corny dad jokes"
        }
      ]
    }
  },
}

  
</script>
