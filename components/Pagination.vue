<template>
  <div class="my-3">
    <button :class="'h-11 mr-4 bg-blue-700 focus:bg-blue-600 py-2 px-3 rounded shadow-sm focus:shadow-md transition duration-500 ease-in-out text-white ' + (currentPage === 1 && ' opacity-50')" :disabled="currentPage === 1" @click="handlePage(currentPage - 1)">
      prev
    </button>
    <span>current: <span class="font-bold">{{currentPage}}</span></span>
    <button :class="'h-11 ml-4 bg-indigo-700 focus:bg-indigo-600 py-2 px-3 rounded shadow-sm focus:shadow-md transition duration-500 ease-in-out text-white ' + (totalPage === currentPage && ' opacity-50')" :disabled="totalPage === currentPage" @click="handlePage(nextPage)">
      next page
    </button>
  </div>
</template>

<script>
  export default {
    name: "Pagination",

    props: {
      currentPage: {
        type: Number,
        default: 1,
      },
      totalPage: {
        type: Number,
        default: 1,
      },
      nextPage: {
        type: Number,
        default: 1,
      },
    },

    methods: {
      handlePage(page) {
        this.$emit("handle-pagination", page)
      }
    },
  }
</script>