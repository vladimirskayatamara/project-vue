<template>
  <div class="form-body">
    <text-input
      :val="formData.name"
      field="name"
      placeholder="Введите наименование товара"
      name="Наименование товара"
      type="text"
      :callback="onChangeInput"
      isRequired
    ></text-input>
    <text-input
      :val="formData.description"
      field="description"
      placeholder="Введите описание товара"
      name="Описание товара"
      type="text"
      :callback="onChangeInput"
      isMulti
    ></text-input>
    <text-input
      :val="formData.productLink"
      field="productLink"
      placeholder="Введите ссылку"
      name="Ссылка на изображение товара"
      type="text"
      :callback="onChangeInput"
      isRequired
    ></text-input>
    <text-input
      :val="formData.price"
      field="price"
      placeholder="Введите цену"
      name="Цена товара"
      type="number"
      :callback="onChangeInput"
      isRequired
    ></text-input>
    <button-component
      :callback="createProduct"
      :isFormValid="isFormValid"
      text="Добавить товар"
    ></button-component>
  </div>
</template>

<script>
import Input from "./Input.vue";
import Button from "./Button.vue";
export default {
  props: {
    onCreate: Function,
  },
  data: function () {
    return {
      formData: {
        name: {
          isError: false,
          value: "",
        },
        description: {
          isError: false,
          value: "",
        },
        productLink: {
          isError: false,
          value: "",
        },
        price: {
          isError: false,
          value: "",
        },
      },
      isFormValid: false,
    };
  },
  components: {
    "text-input": Input,
    "button-component": Button,
  },
  methods: {
    onChangeInput(type, value) {
      this.formData[type] = {
        isError: type !== "description" && value === "",
        value,
      };
      this.isFormValid = Object.keys(this.formData).every(
        (key) => this.formData[key].value !== "" || key === "description"
      );
    },
    createProduct() {
      this.onCreate(this.formData).then(() => {
        this.clearForm();
      });
    },
    clearForm() {
      Object.keys(this.formData).forEach((key) => {
        this.formData[key] = { isError: false, value: "" };
      });
      this.isFormValid = false;
    },
  },
};
</script>

<style lang="less" scoped>
.form-body {
  width: 332px;
  background: #fffefb;
  box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04),
    0px 6px 10px rgba(0, 0, 0, 0.02);
  border-radius: 4px;
  padding: 24px;
  height: 440px;

  @media (max-width: 768px) {
    width: 100%;
  }
}
</style>