<template>
  <div class="avatar">
    <img :src="url">
  </div>
</template>
<script>
export default {
  data() {
    return {
      url: this.$attrs.value
    }
  }
}
</script>
<style scoped>
.avatar {
  display: flex;
  justify-content: center;
}

.avatar img {
  width: 150px;
  height: auto;
  border-radius: 50%;
}
</style>
