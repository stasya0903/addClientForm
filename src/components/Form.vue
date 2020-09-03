<template>
    <div class="container">
        <div class="formCard">
            <div class="formCard_header">
                <p>Добавить Клиента</p>
            </div>
            <form @submit.prevent="someAction" class="form">
                <div class="formLine">
                    <div class="formGroup">
                        <div class="formGroup_input">
                            <label class="textInputLabel" for="lastName">Фамилия</label>
                            <input class="textInput"
                                   id="lastName" type="text"
                                   v-model.trim="$v.client.lastName.$model"
                                   @blur="$v.client.lastName.$touch()"
                                   :class="{ 'errorInput': $v.client.lastName.$error }">
                        </div>

                        <div v-if="$v.client.lastName.$error" class="inputError">
                            Поле обязательно для заполнения
                        </div>
                    </div>
                    <div class="formGroup">
                        <div class="formGroup_input">
                            <label class="textInputLabel" for="name">Имя</label>
                            <input class="textInput"
                                   id="name" type="text"
                                   v-model.trim="$v.client.name.$model"
                                   @blur="$v.client.name.$touch()"
                                   :class="{ 'errorInput': $v.client.name.$error }">
                        </div>
                        <div v-if="$v.client.name.$error" class="inputError">
                            Поле обязательно для заполнения
                        </div>


                    </div>
                    <div class="formGroup">
                        <div class="formGroup_input">
                            <label class="textInputLabel" for="secondName">Отчество</label>
                            <input class="textInput"
                                   id="secondName"
                                   type="text"
                                   v-model.trim="$v.client.secondName.$model"
                                   @blur="$v.client.secondName.$touch()"
                                   :class="{ 'errorInput': $v.client.secondName.$error }">
                        </div>
                        <div v-if="$v.client.secondName.$error" class="inputError">
                            Поле обязательно для заполнения
                        </div>
                    </div>

                </div>
                <div class="formLine">
                    <div class="formGroup">
                        <div class="formGroup_input">
                            <label class="textInputLabel" for="dateOfBirth">Дата рождения</label>
                            <input class="textInput"
                                   id="dateOfBirth" type="date"
                                   v-model.trim="$v.client.dateOfBirth.$model"
                                   @blur="$v.client.dateOfBirth.$touch()"
                                   :class="{ 'errorInput': $v.client.dateOfBirth.$error }">
                        </div>

                        <div v-if="$v.client.dateOfBirth.$error" class="inputError">
                            Поле обязательно для заполнения
                        </div>
                    </div>
                </div>

                <!-- <div>
                     <input type="text" v-model="passportData">
                     <span v-if="$v.passportData.$invalid">
         Серия и номер паспорта должны быть в формате 1234 567890
       </span>
                 </div>-->


                <!--


                  $v.passportDate.$model - объект, при записи данных в который:
                  - Vuelidate присвоит переданное значение полю passportDate
                  - Vuelidate вызовет метод $touch() у объекта $v.passportDate


                -->
                <!-- <div>
                     <input type="text" v-model.lazy="$v.passportDate.$model">
                     <span v-if="$v.passportDate.$error">
         Дата должна быть в формате ДД.ММ.ГГГГ
       </span>
                 </div>-->
                <!--:disabled="$v.$invalid"-->
                <!-- Поле с несколькими ошибками -->


                <button type="submit">
                    Отправить форму
                </button>
            </form>
        </div>
    </div>

</template>

<script>
    import {required} from 'vuelidate/lib/validators';
    import moment from 'moment';

    export default {
        data() {
            return {
                client: {
                    passportData: null,
                    name: '',
                    lastName: '',
                    secondName: '',
                    passportDate: '',
                    dateOfBirth:''
                }
            };
        },
        validations: {
            client: {
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
                },
                lastName: {
                    required,
                },
                secondName: {
                    required,
                },
                dateOfBirth:{
                    required,
                  /*  date_format: 'dd.MM.yyyy'*/
                }

            },
        },
        methods: {
            someAction() {
                console.log(this.client)
            },
        }
    }
</script>


<style>

</style>
