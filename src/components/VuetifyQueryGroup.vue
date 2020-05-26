<template>
  <v-container
  >
    <v-row class="mb-6">
      <v-col md="1">
        <v-select
          id="vqb-match-type"
          v-model="query.logicalOperator"
          :items="labels.matchTypes"
          item-text="id"
          item-value="id"
          label="Match Type"
        >
        </v-select>
        </v-col>
        <v-col md="2">
        <v-btn
          v-if="depth > 1"
          @click="remove"
        ><v-icon>mdi-close</v-icon>
        </v-btn>
        </v-col>

      <v-col md="2">
          <v-select
            v-model="selectedRule"
            :items="rules"
            item-text="label"
            item-value="id"
          >
          </v-select>
      </v-col>
      <v-col md="2">
          <v-btn
            @click="addRule"
          >{{ labels.addRule }}
          </v-btn>
          <v-btn
            v-if="depth < maxDepth"
            @click="addGroup"
          >{{ labels.addGroup }}
          </v-btn>
      </v-col>

      <query-builder-children v-bind="$props"/>
    </v-row>
  </v-container>
</template>

<script>
import QueryBuilderGroup from 'vue-query-builder/dist/group/QueryBuilderGroup.umd.js'
import QueryBuilderRule from './VuetifyQueryRule.vue'

export default {
  name: 'QueryBuilderGroup',

  components: {
    QueryBuilderRule: QueryBuilderRule
  },
  extends: QueryBuilderGroup,
  data () {
    return {
    }
  }
}
</script>

<style>
</style>
