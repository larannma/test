<template>
  <div class="root">
    <div class="root__container">
      <h2 class="form__title">Редактирование структуры</h2>
      <form class="form" @submit.prevent="editStructure" novalidate>
        <p class="form__select-title">Выберите элемент для редактирования</p>
        <select placeholder="Выберите элемент" v-model="selectedItem" id="name" name="name" class="form__name form__input" required>
          <option v-for="item in items" :value="item.value" :key="item.value">{{ item.name }}</option>
        </select>
        <input placeholder="Новое значение" v-model="newItemValue" class="form__input" type="text"/>
        <button type="submit" class="form__submitButton">Редактировать</button>
      </form>
    </div>
  </div>
</template>

<script>
  import { struct } from './utils/struct';

  export default {
    data() {
      return {
        selectedItem: '',
        newItemValue: '',
        items: struct,
      };
    },
    methods: {
      editStructure() {
        const selectedItem = this.items.find(item => item.value === this.selectedItem);
        if (selectedItem) {
          selectedItem.value = this.newItemValue;
        }
        this.newItemValue = '';
        this.selectedItem = '';
        console.log(this.items)
      }
    },
  };
</script>

<style>
* {
  margin: 0;
  box-sizing: border-box;
  padding: 0;
}

.root{
  position: fixed;
  color: #000000;
  justify-content: center;
  align-items: center;
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;
  display: flex;
  font-family: 'Inter', 'Arial', sans-serif;
  font-style: normal;
}

.root__container {
  background-color: rgb(255, 255, 255);
  border-radius: 10px;
  padding: 34px 36px 37px;
  max-width: 500px;
  width: 100%;
  display: flex;
  flex-direction: column;
  box-shadow: 0px 0px 25px rgba(0, 0, 0, 0.25);
  gap: 30px;
}

.form {
  display: flex;
  flex-direction: column;
  gap: 30px;
}

@media screen and (max-width: 600px) {
  .form{
    gap: 10px;
  }
}

.form__title{
  font-size: 30px;
  margin-bottom: 20px;
}

@media screen and (max-width: 600px) {
  .form__title{
    font-size: 15px;
  }
}


.form__submitButton {
  background-color: #0077FF;
  height: 45px;
  border: none;
  border-radius: 2px;
  color: #ffffff;
  cursor: pointer;
  font-size: 20px;
}

.form__input {
  min-height: 45px;
  font-size: 15px;
}

.form__select-title {
  font-size: 20px;
}

@media screen and (max-width: 600px) {
  .root__container{
    max-width: 250px;
  }
}

</style>
