<template>
    <form class="card card-w30" @submit.prevent="submit">
      <div class="form-control">
        <label for="type">Тип блока</label>
        <select id="type" v-model="type">
          <option value="title">Заголовок</option>
          <option value="subtitle">Подзаголовок</option>
          <option value="avatar">Аватар</option>
          <option value="text">Текст</option>
        </select>
      </div>

      <div class="form-control">
        <label for="value">Значение</label>
        <textarea id="value" rows="3" v-model='value'></textarea>
      </div>

      <button class="btn primary" :disabled="!isValid">Добавить</button>
    </form>
</template>

<script>
export default {
    data () {
        return {
            value: '',
            type: 'title'
        }
    },
    emmits: ['add-block'],
    computed: {
        isValid() {
            return this.value.length > 3
        }
    },
    methods: {
      submit () {
        this.$emit('add-block', {
          type: this.type,
          value: this.value,
          id: Date.now()
        })
        this.value = '',
        this.type = 'title'
      }
    }
}
</script>