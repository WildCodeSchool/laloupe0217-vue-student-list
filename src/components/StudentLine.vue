<script>
  export default {
    props: ['student'],
    methods: {
      remove() {
        this.$emit('remove');
      },
    },
  };
</script>

<template lang="pug">
  tr
    td {{student.name}}
    td {{student.first_name}}
    td {{student.age}}
    td
      a.button.is-danger.is-small(@click="remove") Supprimer
</template>

<style>
</style>
