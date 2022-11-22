<template>
  <Demo v-if="isShoeDemo"/>
  <button @click="isShoeDemo = !isShoeDemo">切换隐藏/显示</button>
</template>

<script>
import Demo from './components/Demo'
import { ref } from 'vue'
export default {
  name: 'App',
  components:{Demo},
  setup() {
    let isShoeDemo = ref(true)
    return {
    isShoeDemo
    }
  
  }

 }
</script>

<style>

</style>
