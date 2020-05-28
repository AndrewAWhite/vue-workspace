<template>
  <v-row>
    <v-col>
      Issue Type:
    </v-col>
    <v-col>
        <v-select
          v-model="query.operator"
          :items="rule.operators"
        />
    </v-col>
    <v-col>
        <v-select
          v-model="issue_type"
          v-on:input="update_model"
          :items="issue_types">
        </v-select>
    </v-col>
    <v-col>
      <v-select
        v-if="query.operator==='issue_and_score'"
        v-model="score_operator"
        :items="score_operators"
        v-on:input="update_model"
        />
    </v-col>
    <v-col>
        <v-text-field 
          v-if="query.operator==='issue_and_score'"
          v-model="issue_score"
          type="number"
          v-on:input="update_model" />
    </v-col>
  </v-row>
</template>
<script>
import axios from 'axios'
import token from '../config/portal_token'

export default {
  name: 'IssueTypeRule',
  methods: {
    update_model: function() { 
      if (this.$props.query.operator==='issue_only'){
          this.$emit('input', {
            issue_type: this.$data.issue_type,
          })
      } else if (this.$props.query.operator==='issue_and_score'){
          this.$emit('input', {
            issue_type: this.$data.issue_type,
            operator: this.$data.score_operator,
            score: this.$data.issue_score
          })
      }
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
             return_type: 'diagnostic_issue_type',
             content_type: 'movie'
           }
         }
       ).then((resp) => {
         this.field_names = []
         for (let field of resp.data) this.issue_types.push(field.issue_name)
         })
    }
  },
  props: {
    rule: Object,
    query: Object
  },
  data () {
    return {
      issue_type: '',
      issue_types: [],
      issue_score: 0.0,
      score_operator: '',
      score_operators: ['>=', '<=', '=']
    }
  },
  mounted() {
    this.get_fields()
  }
}
</script>
