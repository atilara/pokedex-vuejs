<template>
  <h1>{{ index }}. {{ name | upperCase }}</h1>
</template>

<script>
export default {
  name: 'Pokemon',
  props: {
    index: Number,
    name: String
  },
  filters: {
    upperCase: function(value) {
      var newName = value[0].toUpperCase() + value.slice(1);
      return newName;
    }
  }
}
</script>

