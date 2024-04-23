// Компонент для вывода навигационных ссылок. Данные для генерации ссылок получает снаружи
<template>
  <nav class="navigation">
    <RouterLink
      v-for="route in routes"
      :key="route.name"
      :to="route.path"
      activeClass="active"
      >{{ route.name }}</RouterLink
    >
  </nav>
</template>

<script>
export default {
  props: {
    routes: {
      type: Array,
      required: true,
    },
  },
};
</script>

<style>
.navigation {
  display: flex;
  justify-content: center;
  gap: 30px;
  padding: 20px;
  font-size: 16px;
  background-color: var(--my-bg);
}

.navigation a {
  color: rgb(0, 162, 255);
}

.active {
  text-decoration: none;
  opacity: 70%;
}
</style>
