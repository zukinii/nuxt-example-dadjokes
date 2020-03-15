<template>
  <div>
      <!-- access the parameter with this -->
      <!-- {{ $route.params.id }} -->
      <nuxt-link to="/jokes">Back to all Jokes</nuxt-link>
      <h2 class="joke-header">{{ joke }}</h2>
      <hr>
      <small>Joke ID: {{ $route.params.id }}</small>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      joke: {}
    }
  },
  async created() {
        const config = {
            headers: {
                'Accept': 'application/json'
            }
        }

        try {
            const res = await axios.get('https://icanhazdadjoke.com/j/' + this.$route.params.id, config);

            this.joke = res.data.joke;
        } catch (error) {
            console.error(error);
        }
  },
  head() {
    console.log(this.joke);
    return {
        title: this.joke.toString().substr(0, 25) + "\u2026",
        meta: [
            {
                hid: 'description',
                name: 'description',
                content: 'Best place for corny dad jokes'
            }
        ]
    }
}
}
</script>

<style>
  .joke-header {
    font-weight: bold;
    margin: 1rem 0;
  }
</style>