// Переиспользуемый компонент-шаблон для стилизации, умеет также выводить заголовок, если получит его пропсом
<template>
  <div class="layout">
    <h3 v-if="!!title">{{ title }}</h3>
    <main class="content">
      <slot />
    </main>
  </div>
</template>

<script>
export default {
  props: {
    title: {
      type: String,
      required: false,
    },
  },
};
</script>

<style>
.layout {
  padding: 0 20px;
  display: flex;
  flex-direction: column;
  flex-grow: 1;
}

.content {
  display: flex;
  flex-grow: 1;
  flex-direction: column;
  gap: 20px;
  justify-content: center;
  align-items: center;
}
</style>
