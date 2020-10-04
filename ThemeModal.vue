<template>
<b-modal
  id="ThemeModal"
  size="sm"
  static
>
<template v-slot:modal-title>Смена темы</template>
<div>
    <div class="auto-wrap">
    <div class="form-check-inline">
  <label class="form-check-label auto-title">
    <input type="radio" class="form-check-input" name="optradio" :checked="!lightMode" @change="changeTheme">Светлая
  </label>
</div>
<div class="form-check-inline">
  <label class="form-check-label auto-title">
    <input type="radio" class="form-check-input" name="optradio" :checked="lightMode" @change="changeTheme">Темная
  </label>
</div>
</div>
  <div class="row inputs_row auto-wrap">
    <p class="auto-title">Автоматически</p>
        <label class="switch">
  <input type="checkbox">
  <span class="slider round"></span>
</label>
  </div>
  <div class="row inputs_row">
      <button type="button" class="btn btn-primary params" data-toggle="collapse" data-target="#demo" @click="showSettings">Настройка параметров</button>
  <div v-if="isShowSet">
      <div class="auto-wrap">
      <p class="auto-title">От заката до рассвета</p>
    <input type="checkbox" class="auto-checkbox">
      </div>
      <label for="" style="font-size: 15px">рассвет</label>
      <input type="time" class="input-time" @change="getSunriseTime">
        <label for="" style="font-size: 15px">закат</label>
      <input type="time" class="input-time" @change="getSunsetTime">
  </div>
  </div>
</div>
  <template v-slot:modal-ok>Сохранить</template>
  <template v-slot:modal-cancel>Отменить</template>
</b-modal>
</template>

<script>
export default {
  name: 'ThemeModal',
  data: function () {
    return {
      lightMode: false,
      isShowSet: false,
      sunriseTime: '',
      sunsetTime: ''
    }
  },
  created () {
    this.lightMode = JSON.parse(localStorage.getItem('lightMode'))
  },
  methods: {
    changeTheme () {
      this.lightMode = !this.lightMode
    },
    showSettings () {
      this.isShowSet = !this.isShowSet
    },
    getSunriseTime (e) {
      this.sunriseTime = e.target.value
      console.log('sunrise', this.sunriseTime)
    },
    getSunsetTime (e) {
      this.sunsetTime = e.target.value
      console.log('sunset', this.sunsetTime)
    }
  },
  watch: {
    lightMode: function () {
      localStorage.setItem('lightMode', JSON.stringify(this.lightMode))
      window.eventBus.$emit('changeLightMode', this.lightMode)
    }
  }
}
</script>

<style scoped>

</style>
