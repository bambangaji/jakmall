<template>
    <div class="group">
        <input :type="type" id="inputValue" :value="inputValue" @input="$emit('update:inputValue', $event.target.value)"
            class="input" :required="isRequiredTest" v-if="isTextArea()">
        <TextArea id="inputValue" :value="inputValue" @input="$emit('update:inputValue', $event.target.value)"
            class="input" :required="isRequiredTest" v-else></TextArea>
        <span class="highlight"></span>
        <span class="bar"></span>
        <label>{{ label }}</label>
    </div>
</template>
  
<script>
export default {
    name: "CustomInput",
    props: {
        label: {
            type: String,
            default: "",
        },
        isRequired: {
            type: String,
            default: 'true'
        },
        type: {
            type: String,
            default: "text",
        },
        inputValue: {
            type: String,
            default: "",
        },
    },
    methods: {
        isTextArea() {
            console.log(this.type);
            return this.type === 'textArea' ? false : true
        }
    },
    computed: {
        isRequiredTest() {
            console.log(this.isRequired);
            return this.isRequired === 'true' ? true : false
        },
    },
};
</script>
<style scoped>
@import "./utility/input.scss";
</style>
