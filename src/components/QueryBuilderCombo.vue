<template>
  <div>
      <select
        v-for="field in orderedFields"
        :key="field.name"
        v-model="field.value"
        v-on:input="update_model">
        <option
          v-for="option in field.options"
          :key="option">
          {{ option }}
        </option>
      </select>
      <button v-on:click="update_options">
        click
      </button>
  </div>
</template>
<script>
const _ = require('lodash')

export default {
  name: 'QueryBuilderCombo',
  methods: {
    update_model: function () {
      const values = {}
      for (const _field of this.$data.fields) {
        values[_field.name] = _field.value
      }
      this.$emit('input', values)
    },
    update_options: function () {
      this.$data.fields.clean_value.options = ['Changed']
    }
  },
  data () {
    return {
      fields: {
        field_name: { index: 1, name: 'field_name', options: ['title', 'release_year', 'director', 'imdb_id'] },
        clean_value: { index: 2, name: 'clean_value', options: ['Interstellar', 'I\'m Gonna Git You Sucka'] }
      }
    }
  },
  computed: {
    orderedFields: function () {
      return _.orderBy(this.$data.fields, 'index')
    }
  }
}
</script>
