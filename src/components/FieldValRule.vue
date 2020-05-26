<template>
  <div>
    <v-card>
      <v-card-title>Search For Clean Value</v-card-title>
      <v-card-text>
        <v-autocomplete
          v-model="clean_value"
          :items="clean_value_items"
          :search-input.sync="clean_value_search"
          item-text="Clean Value"
          label="clean_value"
          return-object
        ></v-autocomplete>
      </v-card-text>
    </v-card>
    {{ this.$store.stored_value }}
  </div>
</template>

<script>
export default {
  name: 'FieldValRule'
}
</script>

<style lang="scss" scoped>

</style>
