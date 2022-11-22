<template>
  <h1>一个人的信息</h1>
  <h2>姓名：{{person.name}}</h2>
  <h2>年龄：{{person.age}}</h2>
  <button @click="test">测试Demo组件的hello事件</button>
  <slot name="asd"></slot>
</template>

<script>
import { reactive } from 'vue'
export default {
  name: 'Demo',
  props:['msg','student'],
  emits:['hello'],
//   beforeCreate() {
//         console.log('---beforeCreate---');
//     },
 setup(props,context) {
    console.log('---setup--',props,context.attrs);
    console.log(context.slots);
   let person = reactive({
     name: '张三',
      age: 20,
 })


  function test(){
    context.emit('hello',666)
  }
    return {
      person,
      test
    }
 }

}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
