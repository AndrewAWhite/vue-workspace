<template>
  <v-row>
    <v-col>
      Output Value:
    </v-col>
    <v-col>
        <v-select
          v-model="output_name"
          v-on:input="update_model"
          :items="output_names">
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
          v-model="output_value"
          v-on:input="update_model" />
    </v-col>
  </v-row>
</template>
<script>
import axios from 'axios'
import token from '../config/portal_token'

export default {
  name: 'OutputValRule',
  methods: {
    update_model: function() { 
      this.$emit('input', {output_name: this.$data.output_name, output_value: this.$data.output_value})
      },
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
             return_type: 'output_name'
           }
         }
       ).then((resp) => {
         this.output_names = []
         for (let field of resp.data) this.output_names.push(field.output_name)
         })
    }
  },
  props: {
    rule: Object,
    query: Object
  },
  data () {
    return {
      output_name: '',
      output_names: [],
      output_value: '',
    }
  },
  mounted() {
    this.get_fields()
  }
}
</script>
