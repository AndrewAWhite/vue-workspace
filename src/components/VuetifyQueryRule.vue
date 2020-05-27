<template>
    <v-row class="mb-6">
        <v-col :offset-md="depth">
        <component
          :is="rule.component"
          :value="query.value"
          @input="updateQuery"
        />
        </v-col>
      <v-col offset-md="5" md="1">
      <!-- Remove rule button -->
      <v-btn  @click="remove"><v-icon>mdi-close</v-icon></v-btn>
      </v-col>
    </v-row>
</template>

<script>
import QueryBuilderRule from 'vue-query-builder/dist/rule/QueryBuilderRule.umd.js'

export default {
  extends: QueryBuilderRule
}
</script>
