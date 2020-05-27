<template>
    <v-row class="mb-6">
          <!--       Custom Components                  -->
        <component
          v-if="rule.type==='custom-component'"
          :is="rule.component"
          :value="query.value"
          @input="updateQuery"
          v-bind:rule="rule"
          v-bind:query="query"
        />
        <v-col md="2">
    <v-label v-if="rule.type!=='custom-component'">{{ rule.label }}</v-label>
        </v-col>
      <v-col md="1">
      <!-- List of operators (e.g. =, !=, >, <) -->
      <v-select
        v-if="typeof rule.operators !== 'undefined' &&  rule.type!=='custom-component'"
        v-model="query.operator"
        :items="rule.operators"
       />
      </v-col>

      <v-col md="4">

      <!-- Basic text input -->
      <v-text-field
        v-if="rule.type === 'text'"
        v-model="query.value"
        type="text"
      />

      <!-- Basic number input -->
      <v-text-field
        v-if="rule.type === 'number'"
        v-model="query.value"
        single-line
        hide-details
        type="number"
      />

      <!-- Datepicker -->
      <v-date-picker
        v-if="rule.type === 'date'"
        v-model="query.value"
      ></v-date-picker>

      <!-- Radio input -->
        <v-radio-group
          v-if="rule.type==='radio'"
        >
          <v-radio
            v-for="choice in rule.choices"
            :key="choice"
            :label="choice.label"
            v-model="query.value"
          ></v-radio>
        </v-radio-group>
      </v-col>

      <!-- Remove rule button -->
      <v-col md="1">
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
