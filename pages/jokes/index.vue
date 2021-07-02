<template>
  <div>
    <SearchJokes @search-joke="handleSearch" />

    <Pagination :next-page="nextPage" :total-page="totalPage" :current-page="currentPage" @handle-pagination="handlePage" />
    
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

    async handlePage(page) {
      const config = {
        headers: {
          Accept: "application/json"
        }
      }
      try {
        const res = await axios.get(`https://icanhazdadjoke.com/search?term$=&page=${page}`, config);

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