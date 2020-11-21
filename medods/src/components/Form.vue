<template>
  <div class="box">
    <div class="form-wrapper">
      <div class="form-tab"></div>
      <div class="form-logo">
        <img src="@/assets/medods-logo.png" alt="logo" />
        <span>Регистрация</span>
      </div>
      <form class="new-client-form" @submit.prevent="onSubmit">
        <div class="new-client-form__container">
          <div class="info-container">
            <div class="field">
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
            <div class="field">
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
            <div class="field">
              <label for="patronymic">Отчество</label>
              <input id="patronymic" type="text" v-model="patronymic" />
            </div>
            <div class="field">
              <label for="birth">Дата рождения</label>
              <input
                id="birth"
                type="text"
                v-model.trim="birth"
                :class="{
                  invalid:
                    ($v.birth.$dirty && !$v.birth.required) ||
                    !$v.birth.validateDate,
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
            <div class="field">
              <label for="phone">Телефон</label>
              <div
                class="phone-container"
                :class="{
                  invalid:
                    ($v.phone.$dirty && !$v.phone.required) ||
                    ($v.phone.$dirty && !$v.phone.validatePhone),
                }"
              >
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
            <div class="field">
              <label for="gender">Пол</label>
              <input id="gender" type="text" v-model="gender" />
            </div>
            <div class="field">
              <label for="male">Группа</label>
              <select
                name="group"
                id="group"
                v-model.trim="group"
                :class="{ invalid: $v.group.$dirty && !$v.group.required }"
              >
                <option value="vip">VIP</option>
                <option value="trouble">Проблемные</option>
                <option value="oms">ОМС</option>
              </select>
              <small v-if="$v.group.$dirty && !$v.group.required"
                >Поле не должно быть пустым</small
              >
            </div>
            <div class="field">
              <label for="doctor">Врач</label>
              <select name="doctor" id="doctor" v-model.trim="doctor">
                <option value="ivanov">Иванов</option>
                <option value="zaharov">Захаров</option>
                <option value="chernysheva">Чернышева</option>
              </select>
            </div>
            <div class="field-checkbox">
              <input v-model="sms" type="checkbox" id="sms" />
              <label for="sms">Не отправлять СМС</label>
            </div>
          </div>
          <div class="document-container">
            <div class="field">
              <label for="zip">Индекс</label>
              <input id="zip" type="text" v-model="zip" />
            </div>
            <div class="field">
              <label for="country">Страна</label>
              <input id="country" type="text" v-model="country" />
            </div>
            <div class="field">
              <label for="area">Область</label>
              <input id="area" type="text" v-model="area" />
            </div>
            <div class="field">
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
            <div class="field">
              <label for="street">Улица</label>
              <input id="street" type="text" v-model="street" />
            </div>
            <div class="field">
              <label for="house">Дом</label>
              <input id="house" type="text" v-model="house" />
            </div>
            <div class="field">
              <label for="doc">Тип документа</label>
              <select
                name="doc"
                id="doc"
                v-model.trim="doc"
                :class="{ invalid: $v.doc.$dirty && !$v.doc.required }"
              >
                <option value="passport">Паспорт</option>
                <option value="cib">Свидетельство о рождении</option>
                <option value="driverLicense">Вод. удостоверение</option>
              </select>
              <small v-if="$v.doc.$dirty && !$v.doc.required"
                >Поле не должно быть пустым</small
              >
            </div>
            <div class="field">
              <label for="serial">Серия</label>
              <input id="serial" type="text" v-model="serial" />
            </div>
            <div class="field">
              <label for="number">Номер</label>
              <input id="number" type="text" v-model="number" />
            </div>
            <div class="field">
              <label for="issue">Дата выдачи</label>
              <input
                id="issue"
                type="text"
                v-model.trim="issue"
                :class="{
                  invalid:
                    ($v.issue.$dirty && !$v.issue.required) ||
                    !$v.issue.validateDate,
                }"
              />
              <small v-if="$v.issue.$dirty && !$v.issue.required"
                >Поле не должно быть пустым</small
              >
              <small v-if="!$v.issue.validateDate"
                >Введите в формате
                {{
                  `${new Date().getDate()}-${new Date().getMonth()}-${new Date().getFullYear()}`
                }}</small
              >
            </div>
            <div class="field area">
              <label for="placement">Кем выдан</label>
              <textarea
                name="placement"
                id="placement"
                cols="30"
                rows="10"
              ></textarea>
            </div>
          </div>
        </div>
        <button type="submit">Отправить</button>
      </form>
      <div class="msg" :class="{ show: msg }">Отправлено</div>
    </div>
  </div>
</template>

<script>
import { required, helpers } from "vuelidate/lib/validators";
const validateDate = helpers.regex("date", /^\d{2}[./-]\d{2}[./-]\d{4}$/);
const validatePhone = (value) => {
  if (/^7/.test(value)) {
    if (value.match(/\d/g).length === 11) {
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
    gender: "",
    group: "",
    doctor: "",
    sms: false,
    zip: "",
    country: "",
    area: "",
    city: "",
    street: "",
    house: "",
    doc: "",
    serial: "",
    number: "",
    placement: "",
    issue: "",
    msg: false,
  }),
  validations: {
    surname: { required },
    name: { required },
    birth: { required, validateDate },
    phone: { required, validatePhone },
    city: { required },
    group: { required },
    doc: { required },
    issue: { required, validateDate },
  },
  methods: {
    onSubmit() {
      if (this.msg === true) {
        return;
      }
      if (this.$v.$invalid) {
        this.$v.$touch();
        return;
      }
      this.msg = true;
      setTimeout(() => {
        this.msg = false;
      }, 3000);
    },
  },
};
</script>

<style lang="scss">
$invalid: rgb(255, 0, 0);
$border: rgb(0, 180, 237);
$back: rgb(210, 229, 236);
$input: rgb(255, 255, 255);
$robo: "Roboto", sans-serif;
$field-w: 250px;

.box {
  position: relative;
  .form-tab {
    width: 45%;
    height: 40px;
    position: relative;
    border-radius: 6px 6px 0 0;
    transform-origin: 0 0;
    background: $back;
    transform: perspective(9px) rotateX(0.93deg) translateZ(-1px);
  }
  .form-logo {
    display: flex;
    align-items: center;
    position: absolute;
    width: 35%;
    height: 40px;
    left: 20px;
    top: 0;
    img {
      width: 30px;
      height: 30px;
    }
    span {
      font-family: "Lobster", cursive;
      font-size: 20px;
      margin-left: 30px;
    }
  }
  .new-client-form {
    display: flex;
    flex-direction: column;
    width: 600px;
    margin-top: -2px;
    background: $back;
    border-radius: 0 5px 5px 5px;
    .new-client-form__container {
      display: flex;
      justify-content: space-between;
      padding: 15px 15px 0 15px;
    }
    .document-container {
      display: flex;
      flex-direction: column;
      align-items: flex-end;
    }
    button {
      width: 100%;
      height: 45px;
      outline: none;
      background: rgb(255, 255, 255);
      border: none;
      border-radius: 0 0 5px 5px;
      cursor: pointer;
      font-family: $robo;
      font-size: 15px;
      transition: background 0.5s ease-in-out;
    }
    button:hover {
      background: $border;
    }
  }
}

.field {
  display: flex;
  width: $field-w;
  height: 37px;
  margin-bottom: 13px;
  flex-direction: column;
  align-items: flex-start;
  justify-content: center;

  label {
    padding-left: 5px;
    font-size: 11px;
    color: rgb(0, 0, 0);
    font-family: $robo;
  }
  input,
  select {
    width: $field-w;
    height: 20px;
    padding: 2px 0 0 3px;
    background: $input;
    border-radius: 3px 3px 0 0;
    outline: none;
    border: none;
    border-bottom: 2px solid $border;
    font-family: $robo;
    font-size: 12px;
  }
  select {
    box-sizing: content-box;
    padding: 2px;
  }
  input.invalid,
  select.invalid {
    border-bottom: 2px solid $invalid;
  }
  small {
    font-size: 10px;
    color: $invalid;
  }
  .phone-container {
    display: flex;
    &:before {
      content: "+";
      width: 7px;
      height: 20px;
      display: flex;
      align-items: center;
      padding-top: 2px;
      padding-left: 3px;
      background: $input;
      border-bottom: 2px solid $border;
      border-top-left-radius: 5px;
      font-size: 12px;
    }
    #phone {
      width: $field-w - 10px;
      border-top-left-radius: 0;
    }
  }
  .phone-container.invalid::before {
    border-bottom: 2px solid $invalid;
  }
}
.field-checkbox {
  display: flex;
  flex-direction: flex-start;
  align-items: center;
  label {
    font-family: $robo;
    font-size: 13px;
  }
}
.field.area {
  height: 80px;
  textarea {
    width: $field-w;
    max-height: 80px;
    resize: none;
    outline: none;
    font-family: $robo;
    background: $input;
    border: none;
    border-radius: 5px 5px 0 0;
    border-bottom: 2px solid $border;
  }
}
.msg {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 120px;
  height: 30px;
  background: rgb(12, 121, 12);
  color: white;
  font-family: $robo;
  border-radius: 10px 0 0 10px;
  position: relative;
  top: -650px;
  float: right;
  visibility: hidden;
  opacity: 0;
}
.show {
  animation: show 3s 1;
}

@keyframes show {
  0% {
    visibility: visible;
    opacity: 0;
  }
  10% {
    opacity: 1;
  }
  70% {
    opacity: 1;
  }
  100% {
    visibility: hidden;
    opacity: 0;
  }
}

@media screen and (max-width: 600px) {
  .box {
    .form-tab {
      width: 65%;
    }
    .form-logo {
      span {
        margin-left: 5px;
      }
    }
    .new-client-form {
      width: 300px;
      max-height: 80vh;
      overflow: scroll;
      .new-client-form__container {
        flex-direction: column;
        align-items: center;
      }
      button {
        min-height: 50px;
      }
      .field-checkbox {
        margin-bottom: 15px;
      }
    }
  }
  .msg {
    top: -450px;
  }
}
</style>
