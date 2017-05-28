<script>
  import axios from 'axios';

  export default {
    data() {
      return {
        student: {
          first_name: '',
          name: '',
          age: null,
        },
      };
    },
    methods: {
      addNewStudent() {
        axios.post('http://localhost:3000/students', this.student)
        .then((res) => {
          this.$emit('add', res.data);
          this.clearNewStudent();
        });
      },
      clearNewStudent() {
        this.student = { first_name: '', name: '', age: null };
      },
    },
  };
</script>

<template lang="pug">
  form(@submit.prevent="addNewStudent()")
    .field
      label.label Firstname
      p.control
        input.input(
          type="text",
          placeholder="Student firstname",
          v-model="student.first_name"
        )
    .field
      label.label Lastname
      p.control
        input.input(
          type="text",
          placeholder="Student name",
          v-model="student.name"
        )
    .field
      label.label Age
      p.control
        input.input(
          type="number",
          placeholder="Student age",
          v-model="student.age"
        )
    .field.has-text-right
      input.button.is-primary(type="submit")
</template>

<style>
</style>
