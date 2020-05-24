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
          label: 'Field Value',
          component: QueryBuilderCombo,
          operators: ['fieldval']
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
