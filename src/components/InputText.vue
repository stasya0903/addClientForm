<template>
    <div class="formGroup" :style="`width:${width};`" >
        <div class="formGroup_input" >
            <label class="textInputLabel" :for="name">{{label}}
                <span v-if="validation.$params.required" class="required">*</span></label>
            <input type="text"
                   class="textInput"
                   :placeholder="placeholder"
                   :id="name"
                   v-model.trim="validation.$model"
                   @blur="makeValidation($event.target.value)"
                   :class="{ 'errorInput': validation.$error }"
                   >
        </div>
        <div v-if="validation.$error" class="inputError">
            <template v-if="paramsArray.includes('required')">
                <p v-show="!validation.required">{{$props.errorMsg['required']}}</p>
            </template>
                <template v-if="validation.$model.length > 0">
                    <template v-for="param in paramsArray.filter((element)=> element !=='required')">
                        <p v-if="(!validation[`${param}`])" :key='param'>{{$props.errorMsg[`${param}`]}}</p>
                    </template>
                </template>
        </div>
    </div>
</template>

<script>
    export default {

        name: "InputText",
        props: {
            label: String,
            placeholder: String,
            name: String,
            validation: Object,
            errorMsg:Object,
            width: {
                type: String,
                default: '22%'
            }
        },
        data() {
            return {
                value: '',
                paramsArray: [...Object.keys(this.validation.$params)],
            }
        },
        methods: {
            makeValidation(value) {
                this.$emit('setValue', value);
                this.validation.$touch();
            },
        }
    }
</script>

<style scoped>

</style>
