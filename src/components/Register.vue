<template>
<div id="register">
  <h2>Форма регистрации</h2>
  <input placeholder="Имя" class="form-control">
  <input placeholder="Фамилия" class="form-control">
  <input placeholder="Электронная почта" class="form-control">
  <input placeholder="Пароль" class="form-control">
  <input placeholder="Подтверждение пароля" class="form-control">
  <button type="submit" class="btn">Зарегистрироваться</button>
   <famous :stories="stories"></famous>
</div>
</template>

<script>
import Famous from './Famous.vue'
export default {
    components: {
      Famous
    },
  created () {
    console.log('регистрация')
},
props: ['stories']
}
</script>