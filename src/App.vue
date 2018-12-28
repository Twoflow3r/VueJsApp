<template>
  <div id="app">
    <!--<img alt="Vue logo" src="./assets/logo.png">-->
    <hello></hello>
    <list :contacts="contacts"></list>
  </div>
</template>

<script>
import Hello from './components/Hello.vue'
import List from './components/List.vue'

export default {
  name: 'app',
  components: {
    Hello,
    List
    
  },
    data() {
    return {
      contacts: [
        {
          
          name: 'Дыка',
          phone: '892312231',
          email: "asdas@mail.ru"
        },
        {
          
          name: 'хныка',
          phone: '13222231',
          email: "asq21das@gmail.ru"
        },
         {
           
          name: 'Поц',
          phone: '792312231',
          email: "a213213sdas@asmail.ru"

        }, 
        {
          name: 'Челик',
          phone: '03',
          email: "34234asdas@mail.ru"
        }, 
        {
         
          name: 'Флагшток',
          phone: '192312231',
          email: "343asdas@mail.ru"
        }, 
        {
         
          name: 'Братишка666',
          phone: '02',
          email: "123asdas@mail.ru"
        }
      ]
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  width: 640px;
  margin: 0 auto;
}
</style>
