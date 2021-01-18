<template>
  <div class="card card-w70">
    <h3 v-if="blocks.length === 0">Добавьте первый блок, чтобы увидеть результат</h3>
    <component v-for="block in blocks" :is="componentName(block.type)" v-bind="block"></component>
  </div>
</template>

<script>
import ProfileTitle from "../components/ProfileTitle"
import ProfileAvatar from "../components/ProfileAvatar"
import ProfileSubtitle from "../components/ProfileSubtitle"
import ProfileText from "../components/ProfileText"

export default {
  props: {
    blocks: {
      type: Array,
      default: []
    }
  },
  computed: {
    componentName() {
      return type => 'profile-' + type
    }
  },
  components: {ProfileTitle, ProfileAvatar, ProfileSubtitle, ProfileText}
}
</script>

<style scoped>

</style>
