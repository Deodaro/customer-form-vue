<template>
  <transition name="modal">
    <div class="modal__wrapper" @click="$emit('close')">
      <div class="modal-content" @click.stop="">
        <div class="modal-body">
          <p>Новый клиент успешно создан!</p>
          <button class="btn btnPrimary" @click="$emit('close')">Ok</button>
        </div>

      </div>
    </div>
  </transition>
  
</template>

<script>
export default {
  mounted () {
    document.body.addEventListener('keyup', e => {
      if (e.key === 'Escape') this.$emit('close')
    })
  },
  computed: {},
  methods: {}
}
</script>

<style lang="scss" scoped>

// animation
.modal-enter {
  opacity: 0
}

.modal-leave-active {
  opacity: 0
}

.modal-enter .modal-content,
.modal-leave-active .modal-content {
  transform: scale(1.2);
}

// static
.modal__wrapper{
  display: flex;
  justify-content: center;
  align-items: center;
  position: fixed;
  top: 0;
  bottom: 0;
  left: 0;
  transition: opacity .2s ease;
  right: 0;
  z-index: 998;
  background-color: rgba(00,00,00,.48);
}

.modal-content {
  position: relative;
  max-width: 600px;
  padding: 20px 18px;
  background-color: #fff;
  border: 1px solid #dcdfe6;
  transition: all .2s ease;
  border-radius: 8px;
  z-index: 999;
  overflow: hidden;
  @media screen and (min-width: 900px) {
    min-width: 500px;
  }
}

.modal-body {
  text-align: center;
  margin: 1.5em;
  p {
    margin-bottom: 20px;
  }
}
</style>
