<template>
  <div class="Child">
    <h3>我是Child组件(父){{x.name}}--{{x.price}}</h3>
    <Son/>
  </div>
</template>

<script>
import {inject} from 'vue'
import Son from './Som'
export default {
  name:'Child',
  components:{Son},
  setup() {
    let x = inject('car')
     return {x}
  }

}
</script>

<style>
.Child{
  background-color: rgb(81, 158, 202);
  padding: 10px;
}
</style>