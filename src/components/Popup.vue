// Переиспользуемый компонент, реализующий поведение popup, контент получает в слот, состояние "Открыт" получает
пропсом, при закрытии отправляет событие родителю
<template>
  <div
    v-if="isOpen"
    @click="close"
    class="backdrop"
  >
    <div
      class="popup"
      @click.stop
    >
      <slot />
    </div>
  </div>
</template>

<script>
export default {
  props: {
    isOpen: {
      type: Boolean,
      required: true,
    },
  },

  emits: {
    closed: null,
  },
  // При монтировании компонента подписываемся на нажатие "Escape", чтоб закрыться
  mounted() {
    document.addEventListener('keydown', this.handleKeydown);
  },
  // Очистка при размонтировании
  beforeUnmount() {
    document.removeEventListener('keydown', this.handleKeydown);
  },

  methods: {
    close() {
      this.$emit('closed');
    },
    handleKeydown(e) {
      if (this.isOpen && e.key === 'Escape') {
        this.close();
      }
    },
  },
};
</script>

<style>
.backdrop {
  position: fixed;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: rgba(0, 0, 0, 0.5);
  z-index: 1;
}

.popup {
  max-width: 500px;
}
</style>
