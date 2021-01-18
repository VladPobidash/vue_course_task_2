<template>
  <div class="container">
    <loader v-if="loading"></loader>
    <p v-else-if="comments.length === 0">
      <button class="btn primary" @click="fetchComments">Загрузить комментарии</button>
    </p>
    <div class="card" v-else>
      <h2>Комментарии</h2>
      <ul class="list">
        <li class="list-item" v-for="comment in comments">
          <div>
            <p><strong>{{ comment.email }}</strong></p>
            <small>{{ comment.text }}</small>
          </div>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import Loader from "@/components/Loader"
import axios from "axios"

export default {
  name: 'comments',
  components: { Loader },
  data() {
    return {
      loading: false,
      comments: []
    }
  },
  methods: {
    async fetchComments() {
      try {
        this.loading = true
        const {data} = await axios.get('https://jsonplaceholder.typicode.com/comments?_limit=15')
        this.comments = Object.keys(data).map(comment => ({
          email: data[comment].email,
          text: data[comment].body
        }))
        this.loading = false
      } catch (e) {
        console.error(e)
      }
    }
  }
}
</script>
