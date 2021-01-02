<template>
  <div id="app">
    <InputNumber v-model="value" :max="10" :min="0" />
  </div>
</template>

<script>
import InputNumber from '@/components/input-number.vue'
export default {
  name: 'App',
  components: {
    InputNumber,
  },
  data(){
    return {
      value:99
    }
  }
}
</script>

<style>

</style>
