<template>
  <div>
    <h1 class="text-3xl md:text-4xl mb-3 md:mb-5 font-bold">Welcome to conry dad jokes app</h1>
  </div>
</template>

<script>
export default {
  name: "Home",

  head(){
    return{
      title: "Welcome to Dad jokes",
      meta: [
        {
          hid: "description",
          name: "description",
          content: "best place for corny dad jokes"
        }
      ]
    }
  }
}
</script>
