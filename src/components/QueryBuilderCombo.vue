<template>
  <div>
      <input
        v-model="val1"
        v-on:input="update_model"
        >
      <input
        v-model="val2"
        v-on:input="update_model"
        >
  </div>
</template>
<script>
export default {
  name: 'QueryBuilderCombo',
  methods: {
    update_model: function () {
      const value = `${this.$data.val1} ${this.$data.val2}`
      this.$emit('input', value)
    }
  },
  data () {
    return {
      val1: '',
      val2: '',
      operators: []
    }
  }
}
</script>
