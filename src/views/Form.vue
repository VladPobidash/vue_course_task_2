<template>
  <form class="card card-w30" @submit.prevent="addBlock">
    <div class="form-control">
      <label for="type">Тип блока</label>
      <select id="type" v-model="blockType">
        <option value="title">Заголовок</option>
        <option value="subtitle">Подзаголовок</option>
        <option value="avatar">Аватар</option>
        <option value="text">Текст</option>
      </select>
    </div>

    <div class="form-control">
      <label for="value">Значение</label>
      <textarea id="value" rows="3" v-model.trim="value"></textarea>
    </div>

    <button class="btn primary" :disabled="isDisabled">Добавить</button>
  </form>
</template>

<script>
export default {
  emits: ['addBlock'],
  data() {
    return {
      blockType: 'title',
      value: ''
    }
  },
  computed: {
    isDisabled() {
      return this.value.length < 4
    }
  },
  methods: {
    addBlock() {
      this.$emit('addBlock', {
        type: this.blockType,
        value: this.value
      })
      this.value = ''
      this.blockType = 'title'
    }
  }
}
</script>
