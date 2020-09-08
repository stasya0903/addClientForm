<template>
    <div class="formGroup selectGroup" :style="`width:${width};`">
        <div class="formGroup_input">
            <label class="textInputLabel" :for="name">{{label}}
                <span v-if="validation.$params.required" class="required">*</span></label>
            <div class="selectInput"
                 @click="openSelect()"
                 :class="{ 'errorInput': validation.$error && !showSelect }">
                <div class="optionsSelected">
                    <span class="optionDefault" v-if="validation.$model.length === 0">Выберите опцию...</span>
                    <template v-else>
                        <span  :class="$props.mult ? 'selectedOptions' : 'selectedOption' "
                               :key="item.index"
                              v-for="item in validation.$model">{{item}}</span>
                    </template>
                </div>
                <div class="selectedArrow">
                    <img v-if="!showSelect" class="selectArrow_img" src="../assets/arrowDown.svg">
                    <img v-if="showSelect" class="selectArrow_img" src="../assets/up-arrow.svg">
                </div>
            </div>
            <select v-show="showSelect"
                    :multiple="mult"
                    :size="$props.options.length"
                    :id="name"
                    v-model.trim="validation.$model"
                    @input="setValue($event.target.value)"
                    class="selectDrop"
            >
                <option v-for="option of this.$props.options"
                        :value="option"
                        :key="option"
                        class="selectOption">{{option}}
                </option>
            </select>
        </div>
        <div v-if="this.validation.$error && !showSelect" class="inputError">
            {{$props.errorMsg['required']}}
        </div>
    </div>
</template>

<script>
    export default {

        name: "InputSelect",
        props: {
            label: String,
            name: String,
            validation: Object,
            options: Array,
            mult: Boolean,
            errorMsg:Object,
            width: {
                type: String,
                default: '22%'
            }
        },
        data() {
            return {
                showSelect: false,
                values: [],
                paramsArray: [...Object.keys(this.validation.$params)]
            }
        },
        methods: {
            setValue(value) {
                this.$emit('setValue', value);

            },
            openSelect(){
                this.showSelect = !this.showSelect;
             this.validation.$touch()
            }

        }
    }
</script>

<style scoped>

</style>
