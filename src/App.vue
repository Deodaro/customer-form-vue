<template>
  <div class="wrapper">
    <div class="wrapper-content">
      
      <section>
        <div class="containter">
          <button class="btn btnPrimary" @click="modalFirst = !modalFirst">Show first modal</button>
          <!-- first modal -->
          <!-- обязательный пропс компонента Modal - title -->
          <!-- передаём его -->
          <modals
            title="First Modal"
            v-if="modalFirst">
            </modals>
        </div>
      </section>

    </div>
  </div>
</template>

<script>

import modals from '@/components/Modal.vue'
export default {
  components: { modals },
  data() {
    return {
      modalFirst: false
    }
  }
}
</script>

<style>
</style>
