<template>
  <div class="Som">
    <h3>我是Son组件(孙){{car.name}}--{{car.price}}</h3>
  </div>
</template>

<script>
import {inject} from 'vue'
export default {
  name:'Som',
  setup() {
    let car = inject('car')
    return {car}
  }

}
</script>

<style>
.Som{
  background-color: rgb(217, 16, 180);
  padding: 10px;
}
</style>