<template>
  <Demo v-if="isShoeDemo"/>
  <button @click="isShoeDemo = !isShoeDemo">切换隐藏/显示</button>
    <texy/>
</template>

<script>
import Demo from './components/Demo'
import texy from './components/texy'
import { ref } from 'vue'
export default {
  name: 'App',
  components:{Demo,texy},
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
