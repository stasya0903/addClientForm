<template>
    <div class="formGroup">
    <div class="inputCheckbox " :style="`width:${width};`">
        <label :for="name" class="textInputLabel">{{$props.label}}</label>
        <input type="checkbox"
               :name="name"
               :id="name"
               v-model.trim="value"
               @change="setUpValue($event.target.value)">
    </div>
    </div>
</template>

<script>
    export default {
        name: "InputCheckbox",
        props: {
            label: String,
            name: String,
            value: Boolean,
            width: {
                type: String,
                default: '90%'
            }
        },
        methods: {
            setUpValue(value) {
                this.$emit('setValue', value);
            },
        }

    }
</script>

<style scoped>

</style>
