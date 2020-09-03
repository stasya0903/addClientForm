<template>
    <form @submit.prevent="someAction()">
     <div class="personal">
      <input type="text" v-model="">
     </div>
        <div>
            <input type="text" v-model="passportData">
            <span v-if="$v.passportData.$invalid">
        Серия и номер паспорта должны быть в формате 1234 567890
      </span>
        </div>
        <div>
            <input type="text" v-model="passportDate" @blur="$v.passportDate.$touch()">
            <span v-if="$v.passportDate.$error">
        Дата должна быть в формате ДД.ММ.ГГГГ
      </span>
        </div>


        <!--
          Поле, которое тоже выведет ошибку после события blur, но с другим подходом

          $v.passportDate.$model - объект, при записи данных в который:
          - Vuelidate присвоит переданное значение полю passportDate
          - Vuelidate вызовет метод $touch() у объекта $v.passportDate

          Модификатор lazy необходим, чтобы присваивание произошло только после blur
        -->
        <div>
            <input type="text" v-model.lazy="$v.passportDate.$model">
            <span v-if="$v.passportDate.$error">
        Дата должна быть в формате ДД.ММ.ГГГГ
      </span>
        </div>

        <!-- Поле с несколькими ошибками -->
        <div>
            <input type="text" v-model="name" @blur="$v.name.$touch()">
            <span v-if="$v.name.$error">
        <template v-if="!$v.name.maxLength">
          Длина имени не должна превышать {{ $v.name.$params.maxLength.max }} символов
        </template>
        <template v-else-if="!$v.name.alpha">
          Имя должно содержать только буквы
        </template>
        <template v-else>
          Имя обязательно для заполнения
        </template>
      </span>
        </div>

        <button type="submit" :disabled="$v.$invalid">
            Отправить форму
        </button>
    </form>
</template>

<script>
    import {required, maxLength} from 'vuelidate/lib/validators';
    import moment from 'moment';

    export default {
        data() {
            return {
                passportData: null,
                name: null,
                passportDate: null,
            };
        },
        validations: {
            // Название поля должно совпадать с полем в data
            passportData: {
                required,
                validFormat: val => /^\d{4} \d{6}$/.test(val),
            },
            passportDate: {
                required,
                validDate: val => moment(val, 'DD.MM.YYYY', true).isValid(),
            },
            name: {
                required,
                maxLength: maxLength(10),
                alpha: val => /^[а-яё]*$/i.test(val),
            },
        },
     someAction(){

     }

    }
</script>


<style>

</style>
