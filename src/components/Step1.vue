<!-- eslint-disable vue/no-mutating-props -->
<template>
    <div class="title__container color_orange pl-3">
        <div>
            <h1>Delivery Details</h1>
        </div>

        <div class="checkbox__dropshipper">
            <input class="dropshipper checkbox__dropshipper__checkbox_color" type="checkbox" id="mike" value="Mike"
                v-model="isDropshipper">
            <label class="checkbox__dropshipper__text_color">Send as Dropshipper</label>
        </div>
    </div>
    <div class="grid-container__content">
        <div>
            <CustomInput label="Email" v-model:inputValue="email" />
            <CustomInput label="Phone Number" v-model:inputValue="phone" />
            <CustomInput label="Delivery Address" v-model:inputValue="deliveryAddress" type="textArea" />
        </div>
        <div>
            <CustomInput label="Dropshipper Name" v-model:inputValue="email" isRequired="false" />
            <CustomInput label="Dropshipper Phone Number" v-model:inputValue="phone" isRequired="false" />
        </div>
    </div>
</template>
  
<script>
import CustomInput from './CustomInput.vue';
export default {
    name: "StepOne",
    props: {
        dropshipperName: {
            type: String,
            default: "",
        },
        email: {
            type: String,
            default: "",
        },
        deliveryAddress: {
            type: String,
            default: "",
        },
        dropshipperPhone: {
            type: String,
            default: "",
        },
        phone: {
            type: String,
            default: "",
        },
    },
    components: { CustomInput }
};
</script>
