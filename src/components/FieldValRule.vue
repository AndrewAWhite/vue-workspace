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
        <v-select
          v-model="query.operator"
          :items="rule.operators"
        />
    </v-col>
    <v-col>
        <v-text-field 
          v-model="clean_value"
          v-on:input="update_model" />
    </v-col>
  </v-row>
</template>
<script>
import axios from 'axios'
import token from '../config/portal_token'

export default {
  name: 'FieldValRule',
  methods: {
    update_model: function() { this.$emit('input', {field_name: this.$data.field_name, clean_value: this.$data.clean_value})},
    get_fields: function(){
       axios(
         {
           method: 'post',
           url: 'https://ampere-analytics.com/api/get/',
           headers: {
             Authorization: token.token
           },
           data:{
             task: 'get',
             return_type: 'input_field'
           }
         }
       ).then((resp) => {
         this.field_names = []
         for (let field of resp.data) this.field_names.push(field.field_name)
         })
    }
  },
  props: {
    rule: Object,
    query: Object
  },
  data () {
    return {
      field_name: '',
      field_names: [],
      clean_value: '',
      operator: ''
    }
  },
  mounted() {
    this.get_fields()
  }
}
</script>
