<template>
<input type="text" v-model="keyWord">
<h2>{{keyWord}}</h2>
</template>

<script>
import { customRef } from 'vue'
export default {
  name: 'App',
  setup() {
    // 自定义ref-->myRef
    function myRef(value){
      let flog
     return customRef((track,trigger)=>{
      return {
        get(){
           track() // 追钟数据
          return value
        },
        set(newValue){
         clearTimeout(flog)
         flog = setTimeout(() => {
          return value = newValue,
          trigger()// 通知vue重新去解析模板
          }, 1000);
        }
      }
     })
      
    }
    let keyWord = myRef('hello')
    return {
    keyWord
    }
  
  }

 }
</script>

<style>

</style>
