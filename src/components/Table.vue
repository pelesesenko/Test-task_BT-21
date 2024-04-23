// Компонент создаёт таблицу из массива с данными, полученного в пропсах
<template>
  <table class="table">
    <tr v-if="rows.length > 0">
      <th>Name</th>
      <th>Value</th>
    </tr>
    <tr v-for="row in rows">
      <td>{{ row[0] }}</td>
      <td>{{ row[1] }}</td>
    </tr>
  </table>
</template>

<script>
export default {
  props: {
    rows: {
      type: Array,
      required: true,
    },
  },
};
</script>

<style scoped>
table {
  table-layout: fixed;
  min-width: 500px;
  border-collapse: collapse;
  border: 2px solid;
}

td,
th {
  border-collapse: collapse;
  border: 1px solid;
  text-align: center;
}
td:first-child,
th:first-child {
  width: 20%;
}
</style>
