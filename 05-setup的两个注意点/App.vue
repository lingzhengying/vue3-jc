<template>
  <Demo @hello="showHello" msg="你好呀" student="桂林信息科技学院">
    <template v-slot:asd>
      <span>你这家伙</span>
    </template>
  </Demo>
</template>

<script>
import Demo from './components/Demo'
export default {
  name: 'App',
  components:{Demo},
  setup() {
    function showHello(value){
      alert(`你好呀，我收到的数据是${value}!`)
    }
    return {
      showHello
    }
  }

 }
</script>

<style>

</style>
