<template>
  <div class="wrapper">
    <div class="wrapper-content">
      
      <section>
        <div class="containter">

          <!-- first modal -->
          <button class="btn btnPrimary" @click="modalFirst = !modalFirst">Show first modal</button>
          <!-- передаём обязательный пропс компонента Modal - title -->
          <modals
            title="First modal"
            v-show="modalFirst"
            @close="modalFirst = false">

            <div slot="body">
              <p>text text text text text text</p>
              <button class="btn btnPrimary" @click="modalFirst = !modalFirst">Well done!</button>
            </div>
          </modals>

          <!-- second modal -->
          <button class="btn btnPrimary" @click="modalSecond.show = !modalSecond.show">Show modal with form</button>
          <modals
            title="Modal with form"
            v-show="modalSecond.show"
            @close="modalSecond.show = false">

            <div slot="body">
              <form @submit.prevent="submitSecondForm">
                <label>Name</label>
                <input type="text" required v-model="modalSecond.name">
                <label>Email</label>
                <input type="email" required v-model="modalSecond.email">
                <button class="btn btnPrimary">Submit</button>
              </form> 
            </div>
          </modals>

          <!-- modal with validate -->
          <button class="btn btnPrimary" @click="modalValidate = !modalValidate">Show modal with form + validate</button>
          <modalValidate v-show="modalValidate" @close="modalValidate = false"/>

          <!-- customer form -->
          <button class="btn btnPrimary" @click="customerForm = !customerForm">Создать клиента</button>
          <customerForm v-show="customerForm" @close="customerForm = false" />

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
