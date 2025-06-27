<script setup>
import { reactive, ref } from 'vue'

const local = reactive({
  lastname: '',
  phone: '',
  date: '',
  time: '',

  errorlastname: false,
  errorphone: false,
  errordate: false,
  errortime: false,

  regname: /^[А-ЯЁ][а-яё]+ [А-ЯЁ][а-яё]+ [А-ЯЁ][а-яё]+$/,
  regphone: /^(\+7\d{10})|(8\d{10})$/,

  check: false,

  results: {}
})


// Функция для проверки формы
function checkingForm() {
  // Если имя пустое - ошибка. Иначе - проверка соотвествия регулярному выражению
  if (!local.lastname) {
    local.errorlastname = true
  } else {
    local.errorlastname = !local.regname.test(local.lastname)
  }

  // Если телефон пустое - ошибка. Иначе - проверка соотвествия регулярному выражению
  if (!local.phone) {
    local.errorphone = true
  } else {
    local.errorphone = !local.regphone.test(local.phone)
  }

  // Если дата пустая - ошибка. Иначе - нет ошибки
  if (!local.date) {
    local.errordate = true
  } else {
    local.errordate = false
  }

  // Если время пустое - ошибка. Иначе - нет ошибки
  if (!local.time) {
    local.errortime = true
  } else {
    local.errortime = false
  }

  // Если все поля ошибок не true - запись результатов в массив, очищение полей, check становится true, чтобы вывести поле с результатов
  if (!local.errorlastname && !local.errorphone && !local.errordate && !local.errortime) {
    local.results = {
      name: local.lastname,
      phone: local.phone,
      date: local.date,
      time: local.time,
    }

    local.check = true

    local.lastname = ''
    local.phone = ''
    local.date = ''
    local.time = ''
  }
  else {
    local.check = false
  }
}

</script>


<template>
  <h2>Забронировать столик</h2>
  <p>Все поля являются обязательными для заполнения</p>
  <div class="inputs">
    <div class="labInp">
      <label for="lastname">Фамилия Имя Отчество</label>
      <input type="text" id="lastname" v-model="local.lastname" placeholder="Иванов Иван Иванович">
      <div class="error" v-if="local.errorlastname">Поле не заполнено или заполнено неверно</div>
    </div>
    <div class="labInp">
      <label for="phone">Телефон</label>
      <input type="tel" id="phone" v-model="local.phone" placeholder="88005553535 или +78005553535">
      <div class="error" v-if="local.errorphone">Поле не заполнено или заполнено неверно</div>
    </div>
    <div class="labInp">
      <label for="date">Дата</label>
      <input type="date" id="date" v-model="local.date" min="2025-06-27">
      <div class="error" v-if="local.errordate">Поле не заполнено или заполнено неверно</div>
    </div>
    <div class="labInp">
      <label for="time">Время</label>
      <input type="time" id="time" v-model="local.time">
      <div class="error" v-if="local.errortime">Поле не заполнено или заполнено неверно</div>
    </div>
  </div>

  <button @click="checkingForm">Забронировать столик</button>

  <div class="res" v-if="local.check">
    <p>ФИО: {{ local.results.name }}</p>
    <p>Телефон: {{ local.results.phone }}</p>
    <p>Дата: {{ local.results.date }}</p>
    <p>Время: {{ local.results.time }}</p>
  </div>
</template>

<style scoped>
.inputs {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

.labInp {
  display: flex;
  flex-direction: column;
  align-items: center;
}

input {
  width: 25rem;
  height: 1.5rem;
}

button {
  margin: 1rem;
}

.error {
  color: red;
}
</style>
