<template>
  <div>
    <SearchJokes @search-joke="handleSearch" />
    
    <div class="my-3">
      <button :class="'h-11 mr-4 bg-blue-700 focus:bg-blue-600 py-2 px-3 rounded shadow-sm focus:shadow-md transition duration-500 ease-in-out text-white ' + (currentPage === 1 && ' opacity-50')" :disabled="currentPage === 1" @click="handlePage(currentPage - 1)">
        prev
      </button>
      <span>current: <span class="font-bold">{{currentPage}}</span></span>
      <button :class="'h-11 ml-4 bg-indigo-700 focus:bg-indigo-600 py-2 px-3 rounded shadow-sm focus:shadow-md transition duration-500 ease-in-out text-white ' + (totalPage === currentPage && ' opacity-50')" :disabled="totalPage === currentPage" @click="handlePage(nextPage)">
        next page
      </button>
    </div>
    
    <Joke v-for="joke of jokes" :id="joke.id" :key="joke.id" :joke="joke.joke" />
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "Jokes",

  async asyncData({$axios}) {
    const config = {
      headers: {
        Accept: "application/json"
      }
    }

    const data = await $axios.$get("https://icanhazdadjoke.com/search",config);
  
    const {results:jokes,total_pages:totalPage, next_page: nextPage, current_page:currentPage} = data;

    return {jokes, totalPage, nextPage, currentPage}
  },

  data() {
    return {
      jokes: [],
      totalPage: 1,
      currentPage: 1,
      nextPage: 1,
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

  methods: {
    async handleSearch(text) {
      const config = {
        headers: {
          Accept: "application/json"
        }
      }

      try {
        const res = await axios.get(`https://icanhazdadjoke.com/search?term=${text}`, config);
        this.jokes = res.data.results;
      } catch (err) {
        throw new Error(err)
      }
    },

    async handlePage(count) {
      const config = {
        headers: {
          Accept: "application/json"
        }
      }
      try {
        const res = await axios.get(`https://icanhazdadjoke.com/search?term=&page=${count}`, config);

        const {results:jokes,total_pages:totalPage, next_page: nextPage, current_page:currentPage} = res.data;

        this.jokes = jokes;
        this.totalPage = totalPage;
        this.nextPage = nextPage;
        this.currentPage = currentPage;
      } catch (err) {
        throw new Error(err)
      }
    }
  },
}
</script>