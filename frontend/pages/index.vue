<template>
  <div class="container">
    <div>
      <Logo />
      <h1 class="title">frontend</h1>
      <div class="links">
        <a
          href="https://nuxtjs.org/"
          target="_blank"
          rel="noopener noreferrer"
          class="button--green"
        >
          Documentation
        </a>
        <a
          href="https://github.com/nuxt/nuxt.js"
          target="_blank"
          rel="noopener noreferrer"
          class="button--grey"
        >
          GitHub
        </a>
      </div>
      <div v-if="error">
        {{ error }}
      </div>
      <div class="posts" v-else>
        <div class="post" v-for="post in posts" :key="post.id">
          <img :src="imageUrlPrefix + post.Image.url" />
          <h1>{{ post.Name }}</h1>
          <p>
            {{ post.Description }}
          </p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      posts: [],
      error: null,
      imageUrlPrefix: process.env.NODE_ENV == 'production' ? '' : 'http://localhost:1337',
    };
  },
  async fetch() {
    try {
      this.posts = await this.$strapi.$posts.find();
    } catch (error) {
      this.error = error;
    }
  },
};
</script>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family: "Quicksand", "Source Sans Pro", -apple-system, BlinkMacSystemFont,
    "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}

.posts {
  display: grid;
  grid-template-columns: repeat(5, 1fr);
}

.post {
  border: 1px solid #ccc;
  padding: 15px;
}

.post img {
  height: 200px;
}
</style>
