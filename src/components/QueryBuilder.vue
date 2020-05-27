<template>
  <div>
   <vue-query-builder :rules="rules" v-model="query">
      <template v-slot:default="slotProps">
        <query-builder-group v-bind="slotProps" :query.sync="query"/>
      </template>
    </vue-query-builder>
    <vue-json-pretty
      :data="query">
    </vue-json-pretty>
  </div>
</template>

<script>
import VueQueryBuilder from 'vue-query-builder'
import QueryBuilderGroup from './VuetifyQueryGroup'
import FieldValRule from './FieldValRule'
import VueJsonPretty from 'vue-json-pretty'

export default {
  name: 'QueryBuilder',
  components: {
    VueQueryBuilder,
    QueryBuilderGroup,
    VueJsonPretty,
  },
  data() {
    return {
      rules: [
        {
          type: 'custom-component',
          id: 'fieldval',
          label: 'FieldVal',
          component: FieldValRule,
          operators: ['='],
          default: {}
        }
      ],

      query: {
        logicalOperator: 'all',
        children: [
          {
            type: 'query-builder-rule',
            query: {
              rule: 'fieldval',
              selectedOperator: '=',
              selectedOperand: 'Fieldval',
              value: {clean_value: 'Ah alright'}
            }
            }
        ]
      }
        
      }
    }
  }
</script>
