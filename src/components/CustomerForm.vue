<template>
  <div class="wrapper">
  <form @submit.prevent="onSubmit">

    <h1>Создание клиента</h1>

    <!-- surname -->
    <div class="form-item" :class="{ errorInput: $v.surname.$error }">
      <label>Фамилия *</label>
      <div class="input-wrapper">
        <p class="errorText" v-if="!$v.surname.required">Пожалуйста, заполните это поле!</p>
        <input
          v-model="surname"
          :class="{ error: $v.surname.$error }"
          @change="$v.surname.$touch()">
      </div>  
    </div>

    <!-- name -->
    <div class="form-item" :class="{ errorInput: $v.name.$error }">
      <label>Имя *</label>
      <div class="input-wrapper">
        <p class="errorText" v-if="!$v.name.required">Пожалуйста, заполните это поле!</p>
        <input
          v-model="name"
          :class="{ error: $v.name.$error }"
          @change="$v.name.$touch()">
      </div>
    </div>
    
    <!-- patronymic -->
    <div class="form-item">
      <label>Отчество</label>
      <div class="input-wrapper">
        <input
          v-model="patronymic"
          @change="$v.patronymic.$touch()">
      </div>
    </div>

    <!-- birthday -->
    <div class="form-item" :class="{ errorInput: $v.birthday.$error }">
      <label>Дата рождения *</label>
      <div class="input-wrapper">
        <p class="errorText" v-if="!$v.birthday.required">Пожалуйста, заполните это поле!</p>
        <input
          type="date"
          class="date"
          v-model="birthday"
          :class="{ error: $v.birthday.$error }"
          @change="$v.birthday.$touch()">
      </div>
    </div>

    <!-- tel -->
    <div class="form-item" :class="{ errorInput: $v.tel.$error }">
      <label>Номер телефона *</label>
      <div class="input-wrapper">
        <p class="errorText" v-if="!$v.tel.required">Пожалуйста, заполните это поле!</p>
        <p class="errorText" v-if="!$v.tel.between">Укажите номер в формате 7999999999</p>
        <p class="errorText" v-if="!$v.tel.minLength">Укажите {{ $v.tel.$params.minLength.min }} цифр в номере телефона</p>
        <input
          type="tel"
          placeholder="7999999999"
          v-model="tel"
          :class="{ error: $v.tel.$error }"
          @change="$v.tel.$touch()">
      </div>
    </div>

    <!-- gender -->
    <div class="form-item">
      <label>Пол</label> 
      <div class="input-wrapper">
        <select
          v-model="gender"
          @change="$v.gender.$touch()">
          <option value="female">женский</option>
          <option value="male">мужской</option>
        </select>
      </div>
    </div>

    <!-- group -->
    <div class="form-item" :class="{ errorInput: $v.group.$error }">
      <label>Группа клиентов *</label>
      <div class="input-wrapper">
        <p class="errorText" v-if="!$v.group.required">Пожалуйста, заполните это поле!</p>
        <select
          name="group"
          class="multiselect"
          v-model="group"
          :class="{ error: $v.group.$error }"
          @change="$v.group.$touch()"
          multiple>
          <option value="vip">VIP</option>
          <option value="difficult">Проблемные</option>
          <option value="oms">ОМС</option>
        </select>
      </div>
    </div>

    <!-- doctor -->
    <div class="form-item">
      <label>Лечащий врач</label>
      <div class="input-wrapper">
        <select
          v-model="doctor"
          @change="$v.doctor.$touch()">
          <option value="Ivanov">Иванов</option>
          <option value="Zakharov">Захаров</option>
          <option value="Chernysheva">Чернышева</option>
        </select>
      </div>
    </div>

    <!-- not send sms-->
    <div class="form-item">
      <label>Не отправлять СМС</label>
      <div class="input-wrapper">
        <input
          class="checkbox"
          type="checkbox"
          v-model="notSms"
          @change="$v.notSms.$touch()">
      </div>
    </div>

    <h2>Адрес</h2>

    <!-- post code -->
    <div class="form-item" :class="{ errorInput: $v.surname.$error }">
      <label>Индекс</label>
      <div class="input-wrapper">
        <p class="errorText" v-if="!$v.postCode.numeric">Пожалуйста, введите правильный индекс!</p>
        <input
          v-model="postCode"
          @change="$v.postCode.$touch()">
      </div>  
    </div>

    <!-- country -->
    <div class="form-item">
      <label>Страна</label>
      <div class="input-wrapper">
        <input
          v-model="country"
          @change="$v.country.$touch()">
      </div>  
    </div>

    <!-- region -->
    <div class="form-item">
      <label>Область</label>
      <div class="input-wrapper">
        <input
          v-model="region"
          @change="$v.region.$touch()">
      </div>  
    </div>

    <!-- city -->
    <div class="form-item" :class="{ errorInput: $v.city.$error }">
      <label>Город *</label>
      <div class="input-wrapper">
        <p class="errorText" v-if="!$v.city.required">Пожалуйста, заполните это поле!</p>
        <input
          v-model="city"
          :class="{ error: $v.city.$error }"
          @change="$v.city.$touch()">
      </div>  
    </div>

    <!-- street -->
    <div class="form-item">
      <label>Улица</label>
      <div class="input-wrapper">
        <input
          v-model="street"
          @change="$v.street.$touch()">
      </div>  
    </div>

    <!-- building number -->
    <div class="form-item">
      <label>Дом</label>
      <div class="input-wrapper">
        <input
          v-model="building"
          @change="$v.building.$touch()">
      </div>  
    </div>

    <h2>Паспорт</h2>

    <!-- document type -->
    <div class="form-item" :class="{ errorInput: $v.documentType.$error }">
      <label>Тип документа *</label>
      <div class="input-wrapper">
        <p class="errorText" v-if="!$v.documentType.required">Пожалуйста, заполните это поле!</p>
        <select
          name=""
          id=""
          v-model="documentType"
          :class="{ error: $v.documentType.$error }"
          @change="$v.documentType.$touch()">
          <option value="passport">Паспорт</option>
          <option value="birthCertificate">Свидетельство о рождении</option>
          <option value="driversLicense">Вод. удостоверение</option>
        </select>
      </div>  
    </div>

    <!-- document series -->
    <div class="form-item">
      <label>Серия</label>
      <div class="input-wrapper">
        <input
          v-model="documentSeries"
          @change="$v.documentSeries.$touch()">
      </div>  
    </div>

    <!-- document number -->
    <div class="form-item">
      <label>Номер</label>
      <div class="input-wrapper">
        <input
          v-model="documentNumber"
          @change="$v.documentNumber.$touch()">
      </div>  
    </div>

    <!-- issuing organisation -->
    <div class="form-item">
      <label>Кем выдан</label>
      <div class="input-wrapper">
        <input
          v-model="issuingOrg"
          @change="$v.issuingOrg.$touch()">
      </div>  
    </div>

    <!-- passport issuing date -->
    <div class="form-item" :class="{ errorInput: $v.issuingDate.$error }">
      <label>Дата выдачи *</label>
      <div class="input-wrapper">
        <p class="errorText" v-if="!$v.issuingDate.required">Пожалуйста, заполните это поле!</p>
        <input
          type="date"
          class="date"
          v-model="issuingDate"
          :class="{ error: $v.issuingDate.$error }"
          @change="$v.issuingDate.$touch()">
      </div>  
    </div>

    <!-- submit button -->
    <button class="btn btnPrimary">Создать</button>

  </form>

  <successMessage v-show="successMessage" @close="successMessage = false" />

  </div>
</template>

<script>
import { required, minLength, numeric, between } from 'vuelidate/lib/validators'
import successMessage from '@/components/UI/SuccessMessage.vue'

export default {
  components: { successMessage },
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
      notSms: '',
      postCode: '',
      country: '',
      region: '',
      city: '',
      street: '',
      building: '',
      documentType: '',
      documentSeries: '',
      documentNumber: '',
      issuingOrg: '',
      issuingDate: '',
      successMessage: false
    }
  },
  validations: {
    surname: { required },
    name: { required },
    patronymic: {},
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
    notSms: {},
    postCode: { numeric },
    country: {},
    region: {},
    city: { required },
    street: {},
    building: {},
    documentType: { required },
    documentSeries: {},
    documentNumber: {},
    issuingOrg: {},
    issuingDate: { required }
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
          notSms: this.notSms,
          postCode: this.postCode,
          country: this.country,
          region: this.region,
          city: this.city,
          street: this.street,
          building: this.building,
          documentType: this.documentType,
          documentSeries: this.documentSeries,
          documentNumber: this.documentNumber,
          issuingOrg: this.issuingOrg,
          issuingDate: this.issuingDate
        }
        console.log(user)
        // reset
        this.surname = ''
        this.name = ''
        this.patronymic = ''
        this.birthday = ''
        this.tel = ''
        this.gender = ''
        this.group = []
        this.doctor = ''
        this.postCode = ''
        this.country = ''
        this.region = ''
        this.city = ''
        this.street = ''
        this.building = ''
        this.documentType = ''
        this.documentSeries = ''
        this.documentNumber = ''
        this.issuingOrg = ''
        this.issuingDate = ''

        this.$v.$reset()
        
        this.successMessage = true
      }
    }
  }
}
</script>

<style lang="scss">

form {
  text-align: center;
}

.form-item {
  display: flex;
  align-items: center;
  margin-bottom: 1%;
  justify-content: center;

  &.errorInput .errorText {
    display: block;
  }
}
.form-item label {
  width: 25vw;
  text-align: right;
  padding-right: 1em;
}
.form-item .errorText {
  display: none;
  margin-bottom: 8px;
  font-size: 13px;
  color: #fc5c65;
}

.input-wrapper {
  width: 50vw;
  padding-right: 25vw;
  display: flex;
  flex-direction: column;
  justify-content: center;
}

.input-wrapper input {
  &.date {
    color: #606266;
  }
  &.checkbox {
    width: 1em;
  }
}

input.error,
select.error {
  border-color: #fc5c65;
}

.multiselect {
  background-image: none;
  padding-bottom: 0;
  border-radius: 0;
}
</style>