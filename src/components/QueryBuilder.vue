<template>
  <div>
   <vue-query-builder :rules="rules" v-model="query">
      <template v-slot:default="slotProps">
        <query-builder-group v-bind="slotProps" :query.sync="query"/>
        <v-btn @click="post_query">
          <v-icon>mdi-send</v-icon>
        </v-btn>
      </template>
    </vue-query-builder>
    
    <vue-json-pretty
      :data="query_result">
    </vue-json-pretty>
  </div>
</template>

<script>
import VueQueryBuilder from 'vue-query-builder'
import QueryBuilderGroup from './VuetifyQueryGroup'
import FieldValRule from './FieldValRule'
import OutputValRule from './OutputValRule'
import IssueTypeRule from './IssueTypeRule'
import VueJsonPretty from 'vue-json-pretty'
import token from '../config/portal_token'
import axios from 'axios'

export default {
  name: 'QueryBuilder',
  components: {
    VueQueryBuilder,
    QueryBuilderGroup,
    VueJsonPretty,
    FieldValRule,
    OutputValRule,
    IssueTypeRule
  },
  methods: {
    post_query: function() {
      this.$data.query_result= {'MESSAGE': 'LOADING'}
      axios.create({baseURL: 'http://127.0.0.1:5000'})(
        {
          method: 'post',
          url: '/diagnostic_filter/', 
          headers: {
             Authorization: token.token
           },
          data: this.$data.query
        }
      ).then(result => {
        this.$data.query_result = result.data
      })
    }
  },
  data() {
    return {
      rules: [
        {
          type: 'custom-component',
          id: 'outputval',
          label: 'Output Value',
          component: OutputValRule,
          operators: ['=', 'contains', 'starts_with', 'ends_with'],
          default: {}
        },
        {
          type: 'custom-component',
          id: 'fieldval',
          label: 'Field Value',
          component: FieldValRule,
          operators: ['=', 'contains', 'starts_with', 'ends_with'],
          default: {}
        },
        {
          type: 'number',
          id: 'mdrec_key',
          label: 'Mdrec Key',
          operators: ['=']
        },
        {
          type: 'custom-component',
          id: 'issue',
          label: 'Issue',
          component: IssueTypeRule,
          operators: ['issue_only', 'issue_and_score']
        }
      ],

      query: {
        logicalOperator: 'all',
        children: [

        ]
      },
      query_result: {}
        
      }
    }
  }
</script>
