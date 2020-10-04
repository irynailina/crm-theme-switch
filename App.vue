<template>
  <div style="display: flex;width: 100%;" :id="isLight">
    <div v-if="$route.name !== 'Login' && $route.name !== 'Logout'">
      <telephony></telephony>
      <call-modal></call-modal>
      <button class="callbutton" v-b-modal.call-modal>
      <i class="fas fa-phone"></i>
      </button>
    </div>
    <router-view></router-view>
  </div>
</template>

<script>
import Telephony from './components/Telephony.vue'
import CallModal from './components/CallModal.vue'
export default {
  data: function () {
    return {
      lightMode: false
    }
  },
  created () {
    window.eventBus.$on('changeLightMode', this.changeLightMode)
    this.lightMode = JSON.parse(localStorage.getItem('lightMode'))
  },
  components: {
    telephony: Telephony,
    'call-modal': CallModal
  },
  methods: {
    changeLightMode (event) {
      this.lightMode = event
    }
  },
  computed: {
    isLight: function () {
      return this.lightMode ? 'test' : false
    }
  }
}
</script>
