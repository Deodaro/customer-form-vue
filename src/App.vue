<template>
  <div class="wrapper">
    <div class="wrapper-content">
      
      <section>
        <div class="containter">

          <!-- customer form -->
          <!-- <button class="btn btnPrimary" @click="customerForm = !customerForm">Создать клиента</button>
          <customerForm v-show="customerForm" @close="customerForm = false" /> -->
          
          <!-- <button class="btn btnPrimary" @click="customerForm = !customerForm">Создать клиента</button>
          <customerForm v-show="customerForm" @close="customerForm = false" />  -->

          <customerForm />
          

        </div>
      </section>

    </div>
  </div>
</template>

<script>

import modals from '@/components/UI/Modal.vue'
import modalValidate from '@/components/ModalValidate.vue'
import customerForm from '@/components/CustomerForm.vue'

export default {
  components: {
    modals,
    modalValidate,
    customerForm
  },
  data() {
    return {
      modalFirst: false,
      modalSecond: {
        show: false,
        name: '',
        email: ''
      },
      modalValidate: false,
      customerForm: false
    }
  },
  methods: {
    submitSecondForm () {
      console.log({
        name: this.modalSecond.name,
        email: this.modalSecond.email
      })
      // после очищаем поля
      this.modalSecond.name = ''
      this.modalSecond.email = ''
      // и закрываем модальное окно
      this.modalSecond.show = false
    }
  }
}
</script>

<style>
</style>
