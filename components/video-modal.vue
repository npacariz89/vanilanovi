<template>
  <div :class="['ww-c-main-modal', modalModifiers]">
    <div class="ww-c-main-modal-wrapper">
      <div v-click-outside="closeModal" class="ww-c-main-modal-container"></div>
    </div>
  </div>
</template>
<script>
import ClickOutside from "vue-click-outside";

export default {
  name: "MainModal",
  directives: {
    ClickOutside
  },

  props: {
    modalModifiers: {
      type: String,
      required: false,
      default: ""
    }
  },
  created() {
    document.documentElement.classList.add("modal-is-open");
  },
  methods: {
    closeModal() {
      this.$emit("closeModal");
      document.documentElement.classList.remove("modal-is-open");
    }
  }
};
</script>

<style>
.modal-enter {
  opacity: 0;
}

.modal-leave-active {
  opacity: 0;
}

.modal-enter .modal-container,
.modal-leave-active .modal-container {
  -webkit-transform: scale(1.1);
  transform: scale(1.1);
}
</style>
