<template>
  <v-container
    class=""
    :class="'depth-' + depth.toString()"
  >
    <v-row class="mb-6">
        <label class="mr-2" for="vqb-match-type">{{ labels.matchType }}</label>
        <v-select
          id="vqb-match-type"
          v-model="query.logicalOperator"
          :items="labels.matchTypes"
          item-text="id"
          item-valye="id"
        >
        </v-select>
        <v-btn
          v-if="depth > 1"
          @click="remove"
        ><v-icon>mdi-close</v-icon>
        </v-btn>
    </v-row>

    <div class="vqb-group-body flex-auto p-5 mb-px">
      <div class="mb-5 flex flex-wrap items-center">
        <div class="form-group flex items-center flex-none">
          <select
            v-model="selectedRule"
            class="inline-block w-auto mr-2 h-10 px-1 py-2 leading-normal gray-500 border border-gray-300 rounded"
          >
            <option v-for="rule in rules" :key="rule.id" :value="rule">{{ rule.label }}</option>
          </select>
          <button
            type="button"
            class="text-white px-3 py-2 rounded bg-gray-600 mr-2"
            @click="addRule"
          >{{ labels.addRule }}</button>
          <button
            v-if="depth < maxDepth"
            type="button"
            class="text-white px-3 py-2 rounded bg-gray-600"
            @click="addGroup"
          >{{ labels.addGroup }}</button>
        </div>
      </div>

      <query-builder-children v-bind="$props"/>
    </div>

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
  extends: QueryBuilderGroup
}
</script>

<style>
</style>
