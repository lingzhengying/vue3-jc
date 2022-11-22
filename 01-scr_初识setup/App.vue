<template>
  <h1>一个人的信息</h1>
  <h2>姓名：{{name}}</h2>
  <h2>年龄：{{age}}</h2>
  <button @click="sayHello()">说话</button>
</template>

<script>

export default {
  name: 'App',
 setup() {
   let name = '张三'
   let age = 18

   function sayHello(){
    alert(`我是${name},我今年${age}岁了，你好呀`)
   }
    return {
      name,
      age,
      sayHello
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
