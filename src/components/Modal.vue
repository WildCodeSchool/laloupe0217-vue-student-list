<script>
  export default {
    props: {
      title: {
        type: String,
      },
      isVisible: {
        type: Boolean,
        default: false,
      },
    },
  };
</script>

<template lang="pug">
transition(name="modal")
  .modal(:class="{ 'is-active': isVisible }")
    .modal-background(@click.stop="$emit('close')")
    .modal-card
      header.modal-card-head(v-if="title")
        p.modal-card-title {{ title }}
        button.delete(@click="$emit('close')")
      section.modal-card-body
        slot
</template>

<style>
  .modal-enter {
    opacity: 0;
  }

  .modal-leave-active {
    opacity: 0;
  }

  .modal-enter .modal-background,
  .modal-leave-active .modal-card {
    -webkit-transform: scale(1.1);
    transform: scale(1.1);
  }
</style>
