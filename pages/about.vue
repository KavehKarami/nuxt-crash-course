<template>
  <div>
    <h1 class="text-4xl md:text-5xl font-bold mb-3 md:mb-5">About dad jokes</h1>
    <p>This is an app that displays conry dad jokes</p>
  </div>
</template>

<script>
  export default {
    name: "About",
    head() {
      return{
        title: "About the App",
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

<style lang="scss" scoped>

</style>