<template>
  <div class="container column">
    <Form @addBlock="addBlock"/>
    <Profile :blocks="blocks" />
  </div>
  <Comments />
</template>

<script>
import Form from "./views/Form"
import Profile from "./views/Profile"
import Comments from "./views/Comments"
import axios from "axios"

export default {
  data() {
    return {
      blocks: []
    }
  },
  async mounted() {
    try {
      const {data} = await axios.get('https://vue-task-2-default-rtdb.europe-west1.firebasedatabase.app/blocks.json')
      if (data !== null) {
        this.blocks = Object.keys(data).map(key => ({
          id: key,
          type: data[key].type,
          value: data[key].value
        }))
      }
    } catch (e) {
      console.error(e);
    }
  },
  methods: {
    async addBlock(newBlock) {
      try {
        await axios.post('https://vue-task-2-default-rtdb.europe-west1.firebasedatabase.app/blocks.json', newBlock)
        this.blocks.push(newBlock)
      } catch (e) {
        console.error(e);
      }
    }
  },
  components: {Form, Profile, Comments}
}
</script>
