<template>
  <div>
   <vue-query-builder :rules="rules" v-model="query">
      <template v-slot:default="slotProps">
        <query-builder-group v-bind="slotProps" :query.sync="query"/>
      </template>
    </vue-query-builder>
    {{ query }}
  </div>
</template>

<script>
import VueQueryBuilder from 'vue-query-builder'
import QueryBuilderGroup from './VuetifyQueryGroup'
import FieldValRule from './FieldValRule'

export default {
  name: 'QueryBuilder',
  components: {
    VueQueryBuilder,
    QueryBuilderGroup
  },
  data() {
    return {
      rules: [
        {
          type: "text",
          id: "vegetable",
          label: "Vegetable"
        },
        {
          type: "radio",
          id: "fruit",
          label: "Fruit",
          choices: [
            { label: "Apple", value: "apple" },
            { label: "Banana", value: "banana" }
          ]
        }
      ],

      query: {
        logicalOperator: "all",
        children: [
          {
            type: "query-builder-group",
            query: {
              logicalOperator: "any",
              children: [
                {
                  type: "query-builder-rule",
                  query: {
                    rule: "vegetable",
                    operator: "contains",
                    operand: "Vegetable",
                    value: null
                  }
                },
                {
                  type: "query-builder-rule",
                  query: {
                    rule: "fruit",
                    operand: "Fruit",
                    value: "banana"
                  }
                }
              ]
            }
          }
        ]
      }
    }
  }
}
</script>
