<template>
  <v-container style="border-left: 4px solid gray">
    <v-row class="mb-6 grey lighten-3">
      <v-col md="1" :offset-md="depth">
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
      
      <v-col offset-md="5" md="1">
      <v-btn
          v-if="depth > 1"
          @click="remove"
        ><v-icon>mdi-close</v-icon>
        </v-btn>
      </v-col>
    </v-row>

    <v-row class="mb-6">
      <v-col md="2"  :offset-md="depth">
          <v-select
            v-model="selectedRule"
            :items="rules"
            item-text="label"
            item-value="id"
          >
          </v-select>
      </v-col>

      <v-col md="2" :offset-md="depth">
          <v-btn
            @click="addRule"
          >{{ labels.addRule }}
          </v-btn>
      </v-col>
      
      <v-col md="2" :offset-md="depth">
          <v-btn
            v-if="depth < maxDepth"
            @click="addGroup"
          >{{ labels.addGroup }}
          </v-btn>
      </v-col>
      </v-row>
      <query-builder-children v-bind="$props"/>
     
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
