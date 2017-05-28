<script>
  import axios from 'axios';
  import Modal from './Modal';

  export default {
    components: {
      Modal,
    },
    props: ['student', 'index'],
    data() {
      return {
        studentToEdit: JSON.parse(JSON.stringify(this.student)),
        showEditModal: false,
      };
    },
    computed: {
      modalTitle() {
        return `Edit ${this.student.first_name} ${this.student.name}`;
      },
    },
    methods: {
      remove() {
        axios.delete(`http://localhost:3000/students/${this.student.id}`)
        .then(() => {
          this.$emit('remove');
        });
      },
      edit() {
        axios.put(`http://localhost:3000/students/${this.student.id}`, this.studentToEdit)
        .then((res) => {
          this.$emit('update', res.data, this.index);
          this.showEditModal = false;
        });
      },
    },
  };
</script>

<template lang="pug">
  tr
    td {{student.name}}
    td {{student.first_name}}
    td {{student.age}}
    td.action
        a.button.is-warning.is-small(@click="showEditModal = true") Edit
        modal(
          :is-visible="showEditModal",
          :title="modalTitle",
          @close="showEditModal = false"
        )
          form(@submit.prevent="edit()")
            .field
              label.label Firstname
              p.control
                input.input(
                  type="text",
                  placeholder="Student firstname",
                  v-model="studentToEdit.first_name"
                )
            .field
              label.label Lastname
              p.control
                input.input(
                  type="text",
                  placeholder="Student name",
                  v-model="studentToEdit.name"
                )
            .field
              label.label Age
              p.control
                input.input(
                  type="number",
                  placeholder="Student age",
                  v-model="studentToEdit.age"
                )
            .field.has-text-right
              input.button.is-primary(type="submit")
        a.button.is-danger.is-outlined.is-small(@click="remove") Delete
</template>

<style>
td.action a.button {
  margin: 0px 3px;
}
</style>
