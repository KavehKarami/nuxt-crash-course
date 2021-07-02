<template>
  <nuxt-link :to="'/jokes/'+id">
    <div class="joke">
      <p>{{joke}}</p>
    </div>
  </nuxt-link>
</template>

<script>
  export default {
    name: "Joke",
    props: {
      joke: {
        type: String,
        default: ""
      },
      id: {
        type: String,
        default: ""
      }
    },
  }
</script>

<style scoped>
.joke {
  padding: 1rem;
  border: 1px dashed #ccc;
  margin: 1rem 0;
}
</style>