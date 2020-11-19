<template>
  <form class="new-client-form" @submit.prevent="onSubmit">
    <div class="input-field">
      <label for="surname">Фамилия</label>
      <input
        id="surname"
        type="text"
        v-model.trim="surname"
        :class="{ invalid: $v.surname.$dirty && !$v.surname.required }"
      />
      <small v-if="$v.surname.$dirty && !$v.surname.required"
        >Поле не должно быть пустым</small
      >
    </div>
    <div class="input-field">
      <label for="name">Имя</label>
      <input
        id="name"
        type="text"
        v-model.trim="name"
        :class="{ invalid: $v.name.$dirty && !$v.name.required }"
      />
      <small v-if="$v.name.$dirty && !$v.name.required"
        >Поле не должно быть пустым</small
      >
    </div>
    <div class="input-field">
      <label for="patronymic">Отчество</label>
      <input id="patronymic" type="text" v-model="patronymic" />
    </div>
    <div class="input-field">
      <label for="birth">Дата рождения</label>
      <input
        id="birth"
        type="text"
        v-model.trim="birth"
        :class="{
          invalid:
            ($v.birth.$dirty && !$v.birth.required) || !$v.birth.validateDate,
        }"
      />
      <small v-if="$v.birth.$dirty && !$v.birth.required"
        >Поле не должно быть пустым</small
      >
      <small v-if="!$v.birth.validateDate"
        >Введите в формате
        {{
          `${new Date().getDate()}-${new Date().getMonth()}-${new Date().getFullYear()}`
        }}</small
      >
    </div>
    <div class="input-field">
      <label for="phone">Телефон</label>
      <div class="phone-container">
        <input
          id="phone"
          type="text"
          v-model.trim="phone"
          :class="{
            invalid:
              ($v.phone.$dirty && !$v.phone.required) ||
              ($v.phone.$dirty && !$v.phone.validatePhone),
          }"
        />
      </div>
      <small v-if="$v.phone.$dirty && !$v.phone.required"
        >Поле не должно быть пустым</small
      >
      <small v-else-if="$v.phone.$dirty && !$v.phone.validatePhone"
        >Неверный формат</small
      >
    </div>
    <div class="input-field">
      <label for="gender">Пол</label>
      <input id="gender" type="text" v-model="gender" />
    </div>
    <div class="input-field">
        <label for="male">Группа</label>
        <select name="group" id="group" v-model.trim="group" :class="{ invalid: $v.group.$dirty && !$v.group.required }">
            <option value="vip">VIP</option>
            <option value="trouble">Проблемные</option>
            <option value="oms">ОМС</option>
        </select>
    </div>
    <div class="input-field">
        <label for="doctor">Группа</label>
        <select name="doctor" id="doctor" v-model.trim="doctor">
            <option value="vip">VIP</option>
            <option value="trouble">Проблемные</option>
            <option value="oms">ОМС</option>
        </select>
    </div>
    <div>
      <label for="sms">Не отправлять СМС</label>
      <input v-model="sms" type="checkbox" id="sms" />
    </div>
    <div class="input-field">
      <label for="zip">Индекс</label>
      <input id="zip" type="text" v-model="zip" />
    </div>
    <div class="input-field">
      <label for="country">Страна</label>
      <input id="country" type="text" v-model="country" />
    </div>
    <div class="input-field">
      <label for="area">Область</label>
      <input id="area" type="text" v-model="area" />
    </div>
    <div class="input-field">
      <label for="city">Город</label>
      <input
        id="city"
        type="text"
        v-model.trim="city"
        :class="{ invalid: $v.city.$dirty && !$v.city.required }"
      />
      <small v-if="$v.city.$dirty && !$v.city.required"
        >Поле не должно быть пустым</small
      >
    </div>
    <div class="input-field">
      <label for="street">Улица</label>
      <input id="street" type="text" v-model="street" />
    </div>
    <div class="input-field">
      <label for="house">Дом</label>
      <input id="house" type="text" v-model="house" />
    </div>
    <button type="submit">asdsad</button>
  </form>
</template>

<script>
import { required, helpers, maxLength } from "vuelidate/lib/validators";
const validateDate = helpers.regex("date", /^\d{2}[./-]\d{2}[./-]\d{4}$/);
const validatePhone = (value) => {
  if (/^7/.test(value)) {
    if (value.match(/\d/g).length === 11) {
      console.log(value.match(/\d/g).length);
      return true;
    } else return false;
  } else return false;
};
export default {
  data: () => ({
    surname: "",
    name: "",
    patronymic: "",
    birth: "",
    phone: "",
    gender: '',
    group:'',
    doctor: '',
    sms: false,
    zip: "",
    country: "",
    area: "",
    city: "",
    street: "",
    house: "",
  }),
  validations: {
    surname: { required },
    name: { required },
    birth: { required, validateDate },
    phone: { required, validatePhone, maxLength: maxLength(25) },
    city: { required },
    group: { required },
  },
  methods: {
    onSubmit() {
      if (this.$v.$invalid) {
        this.$v.$touch();
        console.log("Not Submit");
        return;
      }
      console.log("Submit");
    },
  },
};
</script>

<style lang="scss">
.new-client-form {
  border: 1px solid black;
  padding: 5px;
}

.input-field {
  display: flex;
  width: 200px;
  height: 27px;
  margin-bottom: 8px;
  flex-direction: column;
  align-items: flex-start;
  justify-content: center;

  label {
    font-size: 10px;
    font-weight: 600;
    color: rgb(123, 123, 126);
  }
  input, select {
    width: 200px;
    height: 15px;
    padding: 2px 0 0 3px;
    background: rgb(232, 240, 254);
    border-top-left-radius: 5px;
    border-top-right-radius: 5px;
    outline: none;
    border: none;
    border-bottom: 1px solid rgb(164, 164, 168);
    font-size: 12px;
  }
  select {
    width: 200px;
    box-sizing: content-box;
    padding: 2px;
  }
  .invalid {
    border-bottom: 1px solid red;
    color: red;
  }
  small {
    font-size: 10px;
    color: red;
  }
  .phone-container {
    display: flex;
    &:before {
      content: "+";
      width: 7px;
      height: 15px;
      display: flex;
      align-items: center;
      padding-top: 2px;
      padding-left: 3px;
      background: rgb(232, 240, 254);
      border-bottom: 1px solid rgb(164, 164, 168);
      border-top-left-radius: 5px;
      font-size: 12px;
    }
    #phone {
      width: 190px;
      border-top-left-radius: 0;
    }
  }

}
</style>
