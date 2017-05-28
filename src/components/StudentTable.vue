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
      showAddModal: false,
    };
  },
  methods: {
    getAll() {
      axios.get('http://localhost:3000/students')
      .then((res) => {
        this.students = res.data;
      });
    },
    update(student, index) {
      this.$set(this.students, index, student);
    },
    remove(index) {
      this.students.splice(index, 1);
    },
    addStudent(student) {
      this.students.push(student);
      this.showAddModal = false;
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
      a.button.is-primary(@click="showAddModal = true") Ajouter
    modal(
        title="Add new Student",
        :is-visible="showAddModal",
        @close="showAddModal = false"
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
          :index="index",
          :student="student",
          @update="update",
          @remove="remove(index)"
        )
</template>

<style>
</style>
