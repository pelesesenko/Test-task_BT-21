// Компонент-страница. Существует подход, при котором тут не должно быть вёрстки и стилей. В основном так и сделал, не
стал только заморачиваться с блоком для вывода JSON и кнопкой.
<template>
  <Layout title="Главная страница">
    <Popup
      :is-open="isPopupOpen"
      @closed="isPopupOpen = false"
    >
      <Form @submit="onSubmit" />
    </Popup>
    <div v-if="!!output.length">Это не ошибка, это JSON!</div>
    <div>{{ output }}</div>
    <Table :rows="rows" />
    <button @click="openPopup">Начать</button>
  </Layout>
</template>

<script>
import Layout from '@/components/Layout.vue';
import Popup from '@/components/Popup.vue';
import Form from '@/components/Form.vue';
import Table from '@/components/Table.vue';

export default {
  data() {
    return {
      isPopupOpen: false,
      output: '',
    };
  },
  computed: {
    rows() {
      return this.output ? Object.entries(JSON.parse(this.output)) : [];
    },
  },
  components: {Layout, Popup, Form, Table},
  methods: {
    openPopup() {
      this.isPopupOpen = true;
    },
    onSubmit(data) {
      this.output = data;
      this.isPopupOpen = false;
    },
  },
};
</script>
