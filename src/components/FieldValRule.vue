<template>
  <v-row>
    <v-col>
      Field Value:
    </v-col>
    <v-col>
        <v-select
          v-model="field_name"
          v-on:input="update_model"
          :items="field_names">
        </v-select>
    </v-col>
    <v-col>
        <v-text-field 
          v-model="clean_value"
          v-on:input="update_model" />
    </v-col>
  </v-row>
</template>
<script>

export default {
  name: 'FieldValRule',
  methods: {
    update_model: function() { this.$emit('input', {field_name: this.$data.field_name, clean_value: this.$data.clean_value})
    }
  },
  props: {
    value: Object
  },
  data () {
    return {
      field_name: '',
      field_names: ['title', 'release_year', 'director', 'imdb_id'],
      clean_value: ''
    }
  },
}
</script>
