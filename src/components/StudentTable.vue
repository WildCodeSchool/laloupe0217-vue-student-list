<script>
import axios from 'axios';
import StudentCreator from './StudentCreator';
import StudentLine from './StudentLine';
import Modal from './Modal';

export default {
  components: {
    StudentCreator,
    StudentLine,
    Modal,
  },
  data() {
    return {
      students: [],
      showModal: false,
    };
  },
  methods: {
    getAll() {
      axios.get('http://localhost:3000/students')
      .then((res) => {
        this.students = res.data;
      });
    },
    remove(index) {
      axios.delete(`http://localhost:3000/students/${this.students[index].id}`)
      .then(() => {
        this.students.splice(index, 1);
      });
    },
    addStudent(student) {
      this.students.push(student);
      this.showModal = false;
    },
  },
  mounted() {
    this.getAll();
  },
};
</script>

<template lang="pug">
  .container
    h1.title Student List
    .block.has-text-right
      a.button.is-primary(@click="showModal = true") Ajouter
    modal(
        title="Add new Student",
        :is-visible="showModal",
        @close="showModal = false"
      )
      student-creator(@add="addStudent")
    table.table
      thead
        tr
          th Lastname
          th Firstname
          th Age
          th Actions
      tbody
        student-line(
          v-for='(student, index) in students',
          :student="student",
          @remove="remove(index)"
        )
</template>

<style>
</style>
