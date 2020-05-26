<template>
  <!-- eslint-disable vue/no-v-html -->
    <v-row>
      <!-- List of operands (optional) -->
      
      <v-select
        v-if="typeof rule.operands !== 'undefined'"
        v-model="query.operand"
        :items="rule.operands"
        :label="rule.label"
      >
      </v-select>

      <!-- List of operators (e.g. =, !=, >, <) -->
      <v-select
        v-if="typeof rule.operators !== 'undefined' && rule.operators.length > 1"
        v-model="query.operator"
        :items="rule.operators"
      >
      </v-select>
      <!-- Basic text input -->
      <v-text-field
        v-model="query.value"
        :placeholder="labels.textInputPlaceholder"
      ></v-text-field>
      <!-- Radio input -->
      <v-col v-if="rule.inputType === 'radio'">
        <div
          v-for="choice in rule.choices"
          :key="choice.value"
        >
          <v-input
            :id="'depth' + depth + '-' + rule.id + '-' + index + '-' + choice.value"
            v-model="query.value"
            :name="'depth' + depth + '-' + rule.id + '-' + index"
            type="radio"
            :value="choice.value"
          ></v-input>
          <v-label
            :for="'depth' + depth + '-' + rule.id + '-' + index + '-' + choice.value"
          >{{ choice.label }}</v-label>
        </div>
      </v-col>

      <!-- Remove rule button -->
      <v-btn  @click="remove" v-html="labels.removeRule"><v-icon>mdi-close</v-icon></v-btn>
    </v-row>
</template>

<script>
import QueryBuilderRule from 'vue-query-builder/dist/rule/QueryBuilderRule.umd.js'

export default {
  extends: QueryBuilderRule
}
</script>
