<template>
    <div class="container">
        <div class="formCard">
            <div class="formCard_header">
                <p>Добавить Клиента</p>
            </div>
            <form @submit.prevent="someAction()" class="form">
                <div class="formLine">
                    <input-text label="Фамилия"
                                placeholder="Иванов"
                                name="lastName"
                                @getValue="(value)=>this.client.lastName = value"
                                :validation="$v.client.lastName"
                                :errorMsg="errorMsg">
                    </input-text>
                    <input-text label="Имя"
                                placeholder="Иван"
                                name="firstName"
                                @getValue="(value)=>this.client.name = value"
                                :validation="$v.client.name"
                                :errorMsg="errorMsg">
                    </input-text>
                    <input-text label="Отчество"
                                placeholder="Иванович"
                                name="secondName"
                                @getValue="(value)=>this.client.secondName = value"
                                :validation="$v.client.secondName"
                                :errorMsg="errorMsg">
                    </input-text>
                </div>
                <div class="formLine">
                    <input-text label="Дата Рождения"
                                placeholder="00/00/0000"
                                name="dateOfBirth"
                                @getValue="(value)=>this.client.dateOfBirth = value"
                                :validation="$v.client.dateOfBirth"
                                :errorMsg="errorMsg">
                    </input-text>
                    <input-text label="Телефон"
                                placeholder="+7 000 0000"
                                name="phone"
                                @getValue="(value)=>this.client.phone = value"
                                :validation="$v.client.phone"
                                :errorMsg="errorMsg">
                    </input-text>
                    <div class="formGroup">
                        <div class="formGroup_input formGroup_radio">
                            <label class="textInputLabel">Пол</label>
                            <div class="radioInputGroup">
                                <div class="radioInput">
                                    <label class="textInputLabel" for="female">жен</label>
                                    <input name="gender"
                                           id="female" type="radio"
                                           v-model.trim="client.gender">
                                </div>
                                <div class="radioInput">
                                    <label class="textInputLabel" for="male">муж</label>
                                    <input name="gender"
                                           id="male" type="radio"
                                           v-model.trim="client.gender">
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
                <div class="formLine">
                    <input-select
                            label="Группа клиентов"
                            name="group"
                            @getValue="(value)=>this.client.group = value"
                            :validation="$v.client.group"
                            :errorMsg="errorMsg"
                            :options="clientGroup"
                            :mult="true"
                    ></input-select>
                    <input-select
                            label="Доктор"
                            name="doctor"
                            @getValue="(value)=>this.client.doctor = value"
                            :validation="$v.client.doctor"
                            :errorMsg="errorMsg"
                            :options="doctors"
                            :mult="false"
                    ></input-select>
                    <input-checkbox
                            label="Не отправлять СМС"
                            name="noSms"
                            @getValue="(value)=>this.client.noSms = value"
                            :validation="$v.client.noSms"
                    >
                    </input-checkbox>
                </div>
                <div class="groupInputBox">
                    <div class="groupInputBox_header">Адрес</div>
                    <div class="formLine">
                        <input-text
                                label="Индекс"
                                placeholder="000000"
                                name="zipCode"
                                @getValue="(value)=>this.address.zipCode = value"
                                :validation="$v.address.zipCode"
                                :errorMsg="errorMsg"
                                width="20%"></input-text>
                        <input-text
                                label="Страна"
                                placeholder="Россия"
                                name="country"
                                @getValue="(value)=>this.address.country = value"
                                :validation="$v.address.country"
                                :errorMsg="errorMsg"
                                width="35%"
                                >
                        </input-text>
                        <input-text
                                label="Область"
                                placeholder="Московская область"
                                name="index"
                                @getValue="(value)=>this.address.state = value"
                                :validation="$v.address.state"
                                :errorMsg="errorMsg"
                                width="35%"
                                ></input-text>
                    </div>
                    <div class="formLine">
                        <input-text
                                label="Город"
                                placeholder="Москва"
                                name="city"
                                @getValue="(value)=>this.address.city = value"
                                :validation="$v.address.city"
                                :errorMsg="errorMsg"
                                width="40%"></input-text>
                        <input-text
                                label="Улица"
                                placeholder="Ленина"
                                name="city"
                                @getValue="(value)=>this.address.city= value"
                                :validation="$v.address.city"
                                :errorMsg="errorMsg"
                                width="40%"></input-text>
                        <input-text
                                label="Дом"
                                placeholder="000000"
                                name="index"
                                @getValue="(value)=>this.client.address.index = value"
                                :validation="$v.client.phone"
                                :errorMsg="errorMsg"
                                width="10%"></input-text>
                    </div>
                </div>
                <div class="groupInputBox">
                    <div class="groupInputBox_header">Паспорт</div>
                    <div class="formLine">
                        <input-select
                                label="Группа клиентов"
                                name="group"
                                @getValue="(value)=>this.client.group = value"
                                :validation="$v.client.group"
                                :errorMsg="errorMsg"
                                :options="clientGroup"
                                :mult="true"
                        ></input-select>
                        <input-text
                                label="Страна"
                                placeholder="Россия"
                                name="country"
                                @getValue="(value)=>this.address.country = value"
                                :validation="$v.address.country"
                                :errorMsg="errorMsg"
                                width="35%"
                        >
                        </input-text>
                        <input-text
                                label="Область"
                                placeholder="Московская область"
                                name="index"
                                @getValue="(value)=>this.address.state = value"
                                :validation="$v.address.state"
                                :errorMsg="errorMsg"
                                width="35%"
                        ></input-text>
                    </div>
                    <div class="formLine">
                        <input-select
                                label="Тип документа"
                                name="type"
                                @getValue="(value)=>this.document.type = value"
                                :validation="$v.document.type"
                                :errorMsg="errorMsg"
                                :options="clientGroup"
                                :mult="true"
                        ></input-select>
                        <input-text
                                label="Улица"
                                placeholder="Ленина"
                                name="city"
                                @getValue="(value)=>this.address.city= value"
                                :validation="$v.address.city"
                                :errorMsg="errorMsg"
                                width="40%"></input-text>
                        <input-text
                                label="Дом"
                                placeholder="000000"
                                name="index"
                                @getValue="(value)=>this.client.address.index = value"
                                :validation="$v.client.phone"
                                :errorMsg="errorMsg"
                                width="10%"></input-text>
                    </div>
                </div>



                 <!--<div>
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
    import {helpers} from 'vuelidate/lib/validators'
    import InputText from "@/components/InputText";
    import InputSelect from "@/components/InputSelect";
    import InputCheckbox from "@/components/InputCheckbox";

    const alpha = helpers.regex('alpha', /^[a-zA-Zа-яёА-ЯЁ-]*$/);
    const validDate =  helpers.regex('validDate', /^(0[1-9]|1\d|2\d|3[01])\.(0[1-9]|1[0-2])\.(19|20)\d{2}$/);
    const zipCode = helpers.regex('zipCode', /^\d{5}[-\s]?(?:\d{4})?$/gm);
    const address = helpers.regex('street', /^[a-zA-Zа-яёА-ЯЁ0-9-\b\s]*$/gm)
    const phoneNumber = helpers.regex('phoneNumber',/^(\+7)?9\d{9}$/);
/*    const passportLot = helpers.regex('passportLot',/^\d{4}$/);
      const birthCertLot = helpers.regex('birthCertLot', /^((L?X{0,3}|X[LC])(V?I{0,3}|I[VX]){0,3})-([А-Я]{2})/)
    const documentNumber =helpers.regex('passportNumber', /^\d{6}$/);*/


    export default {
        components: {InputCheckbox, InputSelect, InputText},
        data() {
            return {
                errorMsg: {
                    required: "Поле обязательно для заполнения",
                    phoneNumber: "Введите телефон в формате +7**********",
                    alpha: `Данное поле может содержать только буквы`,
                    validDate: `Дата должна быть в формате ДД.ММ.ГГГГ`,
                    zipCode:`Неправильный формат почтового индекса`,
                    address:`Поле содержит недопустимые символы`,
                    documentLot:'Неверный формат. Серия должа содержать 4 цифры',
                    birthCertLot:'Введите серию свидетельства в формате II-AA',
                    documentNumber:'Неверный формат.Поле должно содержать 6 цифр'

                },
                clientGroup: ["VIP", "Проблемные", "ОМС"],
                doctors: ["Иванов", "Захаров", "Чернышева"],
                documentType:[],
                client: {
                    name: '',
                    lastName: '',
                    secondName: '',
                    dateOfBirth: '',
                    phone: '',
                    gender: '',
                    group: [],
                    doctor: '',
                    noSms: false,
                },
                address: {
                    zipCode: '',
                    country: '',
                    state: '',
                    street:'',
                    city: '',
                    house: '',
                },
                document: {
                    type:[],
                    lot: 0,
                    number:0,
                    issued:'',
                    issuedBy:'',
                }
            };
        },
        validations: {
            client: {
                name: {required, alpha},
                lastName: {required,alpha},
                secondName: {alpha},
                dateOfBirth: {required, validDate},
                phone: {required,phoneNumber},
                group: {required},
                doctor: {alpha},
            },
            address: {
                zipCode: {zipCode},
                country: {address},
                state: {address},
                city:{required,address},
                street:{address},
                building:{address}
            }


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
