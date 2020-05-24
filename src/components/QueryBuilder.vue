<template>
  <div>
    <vue-query-builder
      :rules="rules"
      v-model="query"
    />
    {{ query }}
  </div>
</template>

<script>
import VueQueryBuilder from 'vue-query-builder'
import QueryBuilderCombo from './QueryBuilderCombo'

export default {
  name: 'QueryBuilder',
  data () {
    return {
      rules: [
        {
          type: 'custom-component',
          label: 'Multi',
          component: QueryBuilderCombo,
          operators: ['=']
        }
      ],
      query: {}
    }
  },
  components: {
    VueQueryBuilder
  }
}
</script>
