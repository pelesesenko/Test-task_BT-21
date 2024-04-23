// Корневой компонент. Для постраничной навигации в режиме SPA использована библиотека vue-router
<template>
  <TheNavigation :routes="routes" />
  <RouterView />
</template>

<script>
import TheNavigation from '@/components/TheNavigation.vue';
import {routes} from '@/router';

export default {
  data() {
    return {
      routes,
    };
  },
  components: {TheNavigation},
};
</script>

<style scoped></style>
