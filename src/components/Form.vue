<template>
    <div class="container">
        <div class="formCard">
            <div class="formCard_header">
                <p>Добавить Клиента</p>
            </div>
            <form @submit.prevent="someAction()" class="form">

                <div class="required">* обязательные поля</div>

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
                    <input-text label="Дата Рождения"
                                placeholder="ДД.ММ.ГГГГ"
                                name="dateOfBirth"
                                @getValue="(value)=>this.client.dateOfBirth = value"
                                :validation="$v.client.dateOfBirth"
                                :errorMsg="errorMsg">
                    </input-text>
                </div>
                <div class="formLine">
                    <input-text label="Телефон"
                                placeholder="+7 000 0000"
                                name="phone"
                                @getValue="(value)=>this.client.phone = value"
                                :validation="$v.client.phone"
                                :errorMsg="errorMsg"
                    >
                    </input-text>
                    <div class="formGroup formGroup_radio">
                        <div class="formGroup_input ">
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
                                width="10%"></input-text>
                        <input-text
                                label="Страна"
                                placeholder="Россия"
                                name="country"
                                @getValue="(value)=>this.address.country = value"
                                :validation="$v.address.country"
                                :errorMsg="errorMsg"
                                width="18%"
                        >
                        </input-text>
                        <input-text
                                label="Область"
                                placeholder="Московская область"
                                name="index"
                                @getValue="(value)=>this.address.state = value"
                                :validation="$v.address.state"
                                :errorMsg="errorMsg"
                                width="18%"
                        ></input-text>

                        <input-text
                                label="Город"
                                placeholder="Москва"
                                name="city"
                                @getValue="(value)=>this.address.city = value"
                                :validation="$v.address.city"
                                :errorMsg="errorMsg"
                                width="18%"></input-text>
                        <input-text
                                label="Улица"
                                placeholder="Ленина"
                                name="city"
                                @getValue="(value)=>this.address.street = value"
                                :validation="$v.address.street"
                                :errorMsg="errorMsg"
                                width="17%"></input-text>
                        <input-text
                                label="Дом"
                                placeholder="100"
                                name="index"
                                @getValue="(value)=>this.client.address.building = value"
                                :validation="$v.address.building"
                                :errorMsg="errorMsg"
                                width="10%"></input-text>
                    </div>
                </div>
                <div class="groupInputBox">
                    <div class="groupInputBox_header">Паспорт</div>
                    <div class="formLine">
                        <input-select
                                label="Тип документа"
                                name="type"
                                @getValue="(value)=>clientDocument.type = value"
                                :validation="$v.clientDocument.type"
                                :errorMsg="errorMsg"
                                :options="documentType"
                                width="22%"
                        ></input-select>
                        <input-text
                                label="Серия"
                                placeholder="0000"
                                name="lot"
                                @getValue="(value)=> clientDocument.lot= value"
                                :validation="$v.clientDocument.lot"
                                :errorMsg="errorMsg"
                                width="15%"></input-text>
                        <input-text
                                label="Номер"
                                placeholder="000000"
                                name="number"
                                @getValue="(value)=> clientDocument.number= value"
                                :validation="$v.clientDocument.number"
                                :errorMsg="errorMsg"
                                width="17%"></input-text>

                        <input-text
                                label="Дата выдачи"
                                placeholder="ДД.ММ.ГГГГ"
                                name="issued"
                                @getValue="(value)=> clientDocument.issued= value"
                                :validation="$v.clientDocument.issued"
                                :errorMsg="errorMsg"
                                width="20%"></input-text>
                        <input-text
                                label="Кем Выдан"
                                placeholder="ОВД Московсого р-на"
                                name="issuedBy"
                                @getValue="(value)=> clientDocument.issuedBy = value"
                                :validation="$v.clientDocument.issuedBy"
                                :errorMsg="errorMsg"
                                width="18%"></input-text>


                    </div>
                </div>
                <div class="submitStatus" v-show="submitStatus">{{submitStatus}} <span @click="clearStatus()">X</span>
                </div>
                <div class="submitContainer">

                    <button type="submit" class="submitBtn">
                        Добавить
                    </button>
                </div>
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
    const validDate = helpers.regex('validDate', /^(0[1-9]|1\d|2\d|3[01])\.(0[1-9]|1[0-2])\.(19|20)\d{2}$/);
    const zipCode = helpers.regex('zipCode', /^\d{5}[-\s]?(?:\d{4})?$/gm);
    const street = helpers.regex('street', /^(\d*)([a-zA-ZА-яа-я-]+)(\s)*([a-zA-ZА-яа-я\s]+)?$/);
    const building = helpers.regex("building", /^(\d+)([a-zA-ZА-яа-я-]*)$/gm);
    const phoneNumber = helpers.regex('phoneNumber', /^(\+7)?9\d{9}$/);
    const documentLot = helpers.regex('passportLot', /^\d{4}$/);
    const birthCertLot = helpers.regex('birthCertLot', /^((L?X{0,3}|X[LC])(V?I{0,3}|I[VX]){0,3})-([А-Я]{2})/);
    const documentNumber = helpers.regex('passportNumber', /^\d{6}$/);


    export default {
        components: {InputCheckbox, InputSelect, InputText},
        data() {
            return {
                errorMsg: {
                    required: "Поле обязательно для заполнения",
                    phoneNumber: "Введите телефон в формате +7**********",
                    alpha: `Допустимы только буквы и знак дефиса`,
                    validDate: `Дата должна быть в формате ДД.ММ.ГГГГ`,
                    zipCode: `Неверный формат`,
                    street: `Неверный формат названия улицы`,
                    building: 'Неверный формат',
                    documentLot: 'Введите 4 цифры серии',
                    birthCertLot: 'Введите серию в формате II-AA',
                    documentNumber: 'Введите 6 цифр номера документа',
                },
                submitStatus: '',
                submitMessage: '',
                clientGroup: ["VIP", "Проблемные", "ОМС"],
                doctors: ["Иванов", "Захаров", "Чернышева"],
                documentType: ['Паспорт', 'Св-во о рождении', 'Вод. удостоверение'],
                client: {
                    name: '',
                    lastName: '',
                    secondName: '',
                    dateOfBirth: '',
                    phone: '',
                    gender: '',
                    group: [],
                    doctor: [],
                    noSms: false,
                },
                address: {
                    zipCode: '',
                    country: '',
                    state: '',
                    street: '',
                    city: '',
                    building: '',
                },
                clientDocument: {
                    type: [],
                    lot: '',
                    number: '',
                    issued: '',
                    issuedBy: '',
                }
            };
        },
        validations() {
            return {
                client: {
                    name: {required, alpha},
                    lastName: {required, alpha},
                    secondName: {alpha},
                    dateOfBirth: {required, validDate},
                    phone: {required, phoneNumber},
                    group: {required},
                    doctor: {alpha},
                },
                address: {
                    zipCode: {zipCode},
                    country: {alpha},
                    state: {alpha},
                    city: {required, alpha},
                    street: {street},
                    building: {building}
                },
                clientDocument: {
                    type: {required},
                    lot: this.dynamicRule,
                    number: {documentNumber},
                    issued: {required, validDate},
                    issuedBy: {alpha}
                }
            }
        },
        computed:{
            dynamicRule(){
                return (this.clientDocument.type === 'Св-во о рождении') ? {birthCertLot} : {documentLot}
            }
        },
        methods: {
            someAction() {
                this.$v.$touch();
                if (this.$v.$invalid) {
                    this.submitStatus = 'Проверьте введеные данные'
                } else {
                    this.submitStatus = 'Отправка.Пожалуйста подождите';
                    this.$v.$reset();
                    this.clearData();
                    setTimeout(() => {
                        this.submitStatus = 'Пользователь успешно создан';
                        let clientInfo = {
                            client: Object.assign({doctor: this.client.doctor[0],},
                                {...this.client,},
                            ),
                            address: {...this.address},
                            document: Object.assign({type: this.clientDocument.type[0]},
                                {...this.clientDocument})
                        };
                        console.log(JSON.stringify(clientInfo));
                    }, 500)
                }
            },
            clearStatus() {
                this.submitStatus = '';
            },
            clearData() {
                this.client = {
                    name: '',
                    lastName: '',
                    secondName: '',
                    dateOfBirth: '',
                    phone: '',
                    gender: '',
                    group: [],
                    doctor: [],
                    noSms: false,
                };
                this.address = {
                    zipCode: '',
                    country: '',
                    state: '',
                    street: '',
                    city: '',
                    building: '',
                };
                this.clientDocument = {
                    type: [],
                    lot: '',
                    number: '',
                    issued: '',
                    issuedBy: '',
                }
            }
        }
    }
</script>


<style>

</style>
