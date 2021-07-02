<template>
  <div class="w-5/12 flex justify-start items-center">
    <input v-model="search" class="h-11 flex-grow shadow-sm focus:shadow transition duration-500 ease-in-out appearance-none border rounded py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline" type="text" @keypress.enter="onSubmit">
    <button class="h-11 ml-4 bg-red-700 focus:bg-red-600 py-2 px-3 rounded shadow-sm focus:shadow-md transition duration-500 ease-in-out text-white" @click="onSubmit">search</button>
  </div>
</template>

<script>
  export default {
    name:"SearchJokes",

    data() {
      return {
        search: ""
      }
    },

    methods: {
      onSubmit() {
        this.$emit("search-joke", this.search);
        this.search = ""
      }
    },
  }
</script>
