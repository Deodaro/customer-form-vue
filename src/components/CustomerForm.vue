<template>
  <form @submit.prevent="onSubmit">

    <h1>Создание клиента</h1>
    <!-- <p><span>Поля, отмеченные *, обязательны для заполнения.</span></p> -->

    <!-- surname -->
    <div class="form-item" :class="{ errorInput: $v.surname.$error }">
      <label>Фамилия *</label>
      <p class="errorText" v-if="!$v.surname.required">Пожалуйста, заполните это поле!</p>
      <input
        v-model="surname"
        :class="{ error: $v.surname.$error }"
        @change="$v.surname.$touch()">
    </div>

    <!-- name -->
    <div class="form-item" :class="{ errorInput: $v.name.$error }">
      <label>Имя *</label>
      <p class="errorText" v-if="!$v.name.required">Пожалуйста, заполните это поле!</p>
      <input
        v-model="name"
        :class="{ error: $v.name.$error }"
        @change="$v.name.$touch()">
    </div>
    
    <!-- patronymic -->
    <div class="form-item">
      <label>Отчество</label>
      <input
        v-model="patronymic"
        @change="$v.patronymic.$touch()">
    </div>

    <!-- birthday -->
    <div class="form-item" :class="{ errorInput: $v.birthday.$error }">
      <label>Дата рождения *</label>
      <p class="errorText" v-if="!$v.birthday.required">Пожалуйста, заполните это поле!</p>
      <input
        type="date"
        v-model="birthday"
        :class="{ error: $v.birthday.$error }"
        @change="$v.birthday.$touch()">
    </div>

    <!-- tel -->
    <div class="form-item" :class="{ errorInput: $v.tel.$error }">
      <label>Номер телефона *</label>
      <p class="errorText" v-if="!$v.tel.required">Пожалуйста, заполните это поле!</p>
      <!-- <p class="errorText" v-if="!$v.tel.numeric">Укажите номер в формате 7 999 999 9999</p> -->
      <!-- <p class="errorText" v-if="!$v.tel.isPhone">Укажите номер в формате 7 999 999 9999</p> -->
      <p class="errorText" v-if="!$v.tel.between">Укажите номер в формате 7999999999</p>
      <!-- <p class="errorText" v-if="!$v.tel.tel">Указан неверный номер телефона</p> -->
      <p class="errorText" v-if="!$v.tel.minLength">Укажите {{ $v.tel.$params.minLength.min }} цифр в номере телефона</p>
      <!-- <p class="errorText" v-if="!$v.tel.minLength">Укажите номер в формете +7 (___) ___ ____</p> -->
      <input
        type="tel"
        placeholder="7999999999"
        v-model="tel"
        :class="{ error: $v.tel.$error }"
        @change="$v.tel.$touch()">
    </div>

    <!-- gender -->
    <div class="form-item">
      <label>Пол</label> 
        <select
          v-model="gender"
          @change="$v.gender.$touch()">
          <option value="female">женский</option>
          <option value="male">мужской</option>
        </select>
    </div>

    <!-- group -->
    <div class="form-item" :class="{ errorInput: $v.group.$error }">
      <label>Группа клиентов *</label>
      <p class="errorText" v-if="!$v.group.required">Пожалуйста, заполните это поле!</p>
      <select
        multiple
        name=""
        id=""
        v-model="group"
        :class="{ error: $v.group.$error }"
        @change="$v.group.$touch()">
        <option value="vip">VIP</option>
        <option value="difficult">Проблемные</option>
        <option value="oms">ОМС</option>
      </select>
    </div>

    <!-- doctor -->
    <div class="form-item">
      <label>Лечащий врач</label>
      <select
        v-model="doctor"
        @change="$v.doctor.$touch()">
        <option value="Ivanov">Иванов</option>
        <option value="Zakharov">Захаров</option>
        <option value="Chernysheva">Чернышева</option>
      </select>
    </div>

    <!-- not send sms-->
    <div class="form-item">
      <label>Не отправлять СМС</label>
      <input
        type="checkbox"
        v-model="notSms"
        @change="$v.notSms.$touch()">
    </div>

    <!-- submit button -->
    <button class="btn btnPrimary">Submit</button>
  </form>
</template>

<script>
import { required, minLength, numeric, between } from 'vuelidate/lib/validators'
import modal from '@/components/UI/Modal.vue'

export default {
  components: { modal },
  data () {
    return {
      surname: '',
      name: '',
      patronymic: '',
      birthday: '',
      tel: '',
      gender: '',
      group: [],
      doctor: '',
      notSms: ''
    }
  },
  validations: {
    surname: { required },
    name: { required },
    birthday: { required },
    tel: {
      required,
      numeric,
      minLength: minLength(11),
      between: between(70000000000, 79999999999)
    },
    gender: {},
    group: { required },
    doctor: {},
    notSms: {}
  },
  methods: {
    onSubmit () {
      this.$v.$touch()
      if (!this.$v.$invalid) {
        const user = {
          surname: this.surname,
          name: this.name,
          patronymic: this.patronymic,
          birthday: this.birthday,
          tel: this.tel,
          gender: this.gender,
          group: this.group,
          doctor: this.doctor,
          notSms: this.notSms
        }
        console.log(user)
        // reset and close
        this.surname = ''
        this.name = ''
        this.patronymic = ''
        this.birthday = ''
        this.tel = ''
        this.gender = ''
        this.group = []
        this.doctor = ''
        this.$v.$reset()
        this.$emit('close')
      }
    }
  }
}
</script>

<style lang="scss">
.form-item .errorText {
  display: none;
  margin-bottom: 8px;
  font-size: 13px;
  color: #fc5c65;
}
.form-item {
  &.errorInput .errorText {
  display: block;
  }
}
input.error {
  border-color: #fc5c65;
}
</style>