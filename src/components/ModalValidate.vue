<template>
  <modal
    title="Modal with form"
    @close="$emit('close')">
    <!-- body -->
    <div slot="body">
      <form @submit.prevent="">
        <!-- класс errorInput появится только тогда, когда есть ошибки (когда error = true) -->
        <!-- name -->
        <div class="form-item" :class="{ errorInput: $v.name.$error }">
          <label>Name:</label>
          <p class="errorText" v-if="!$v.name.required">Field is required!</p>
          <p class="errorText" v-if="!$v.name.minLength">Name must have at least {{ $v.name.$params.minLength.min }}!</p>
          <input
            v-model="name"
            :class="{ error: $v.name.$error }"
            @change="$v.name.$touch()">
        </div>

        <!-- email -->
        <div class="form-item">
          <label>Email:</label>
          <input v-bind="email">
          <button class="btn btnPrimary">Submit</button>
        </div>
     
      </form> 
    </div>
  </modal>
</template>

<script>
import { required, minLength, email } from 'vuelidate/lib/validators'

import modal from '@/components/UI/Modal.vue'

export default {
  components: { modal },
  data () {
    return {
      name: '',
      email: ''
    }
  },
  validations: {
    name: {
      required,
      minLength: minLength(4)
    },
    email: {
      required,
      email
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