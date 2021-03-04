<template>
  <div>
    <SearchJokes v-on:search-text="searchText" />
    <Joke
      v-for="joke in jokes"
      :key="joke.id"
      :id="joke.id"
      :joke="joke.joke"
    />
    <p></p>
  </div>
</template>

<script>
import axios from "axios";
import Joke from "@/components/Joke.vue";
import SearchJokes from "@/components/SearchJokes.vue";

export default {
  data() {
    return {
      jokes: []
    };
  },
  components: { Joke, SearchJokes },
  async created() {
    const config = {
      headers: {
        Accept: "application/json"
      }
    };

    try {
      const res = await axios.get("https://icanhazdadjoke.com/search", config);
      // console.log(res.data);
      this.jokes = res.data.results;
    } catch (err) {
      console.log(err);
    }
  },
  methods: {
    async searchText(text) {
      const config = {
        headers: {
          Accept: "application/json"
        }
      };

      try {
        const res = await axios.get(
          `https://icanhazdadjoke.com/search?term=${text}`,
          config
        );
        // console.log(res.data);
        this.jokes = res.data.results;
      } catch (err) {
        console.log(err);
      }
    }
  },
  head() {
    return {
      title: "Dad Jokes",
      meta: [
        {
          hid: "",
          name: "description",
          content: "Best place for corny dad jokes"
        }
      ]
    };
  }
};
</script>
