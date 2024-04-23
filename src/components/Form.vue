// Динамически генерируем поля ввода в цикле с 'v-for', реализуем двустороннее связывание значений инпутов и
соотвествующих значений в состоянии компонента с 'v-model', атрибуты с динамическими значениями задаём с ':',
устанавливаем метод компонента в качестве обработчика клика по кнопке '@click="onSubmit"'
<template>
  <form class="form">
    <div
      class="field"
      v-for="field in $options.fields"
      :key="field.name"
    >
      <label
        class="label"
        :for="field.name"
        >{{ field.name }}
      </label>
      <input
        :id="field.name"
        :name="field.name"
        :type="field.type"
        v-model="formData[field.name]"
      />
    </div>
    <button
      type="submit"
      @click="onSubmit"
      :disabled="!isFieldsFilled"
    >
      Отправить
    </button>
  </form>
</template>

<script>
export default {
  // Данные для генерации полей ввода, могут быть получены снаружи, через пропсы, например
  fields: [
    {name: 'text1', type: 'text'},
    {name: 'text2', type: 'text'},
    {name: 'text3', type: 'text'},
    {name: 'text4', type: 'text'},
    {name: 'checkbox', type: 'checkbox'},
  ],
  data() {
    return {
      formData: this.initForm(this.$options.fields),
    };
  },
  computed: {
    // Вычисляемое значение - заполнены ли все текстовые поля формы
    isFieldsFilled() {
      for (let key in this.formData) {
        if (this.formData[key] === '') return false;
      }
      return true;
    },
  },

  methods: {
    onSubmit(e) {
      e.preventDefault();
      // Отправка события родительскому компоненту с полезной нагрузкой - сериализованными данными формы
      this.$emit('submit', JSON.stringify(this.formData));
      this.formData = this.initForm(this.$options.fields);
    },
    // метод для инициализации в состоянии полей, соответствующих полям ввода, применяется также для сброса значений формы после отправки
    initForm(fields) {
      return fields.reduce((acc, cur) => ((acc[cur.name] = cur.type === 'text' ? '' : false), acc), {});
    },
  },
};
</script>
// Стили с ограниченной областью видимости (scoped). Здесь и в навигации использована css-переменная --my-bg,
объявленная в корневом style.css
<style scoped>
.form {
  display: flex;
  padding: 20px 14px 20px 20px;
  flex-wrap: wrap;
  gap: 10px;
  background-color: var(--my-bg);
}

.field {
  display: flex;
  flex-direction: column;
  align-items: start;
}

input {
  margin: 0;
}
input:not([type='checkbox']) {
  width: 220px;
}

button {
  align-self: flex-end;
  margin-left: auto;
}

@media (max-width: 600px) {
  .form {
    flex-direction: column;
    align-items: start;
    padding: 16px;
  }
}
</style>
