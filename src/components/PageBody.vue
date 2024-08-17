<template>
    <div>
        <h3 v-html="$options.filters.highlightFilter(text, userRegex, $style)"></h3>
        <v-text-field
        outlined
        v-model="userRegex"
        placeholder="Enter Regex"
      >
        <template v-slot:prepend>
            /
        </template>
        <!-- farraday's had append-outer that wasn't displaying for me -->
        <template v-slot:append>
            /
        </template>
      </v-text-field>
  </div>
</template>

<script>
export default {
  data () {
    return {
      text: 'Some text more text for everyone',
      userRegex: ''
    }
  },
  filters: {
    highlightFilter (value, userRegex, $style) {
      const regex = new RegExp(userRegex, 'g')
      const newValue = value.replace(
        regex, (text) => `<span class="${$style.highlight}">${text}</span>`
      )
      // Farraday had let instead of const above but let resulted in errors for me
      return newValue
    }
  }
}
</script>

<style lang="sass" module>
.highlight
  background-color: yellow
</style>
