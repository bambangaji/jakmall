<template>
  <div class="app bg_color_white_peach">
    <div class="container__step bg_color_white_peach">
      <div v-for="(s, index) in step" :key="index">
        <div v-if="currentStep >= s" class="display_flex">
          <h3 class="step color_white bg_color_orange">{{ s }}</h3>
          <h4 v-if="s === 1" class="step__step_details color_orange">Delivery ></h4>
          <h4 v-if="s === 2" class="step__step_details color_orange">Payment ></h4>
          <h4 v-if="s === 3" class="step__step_details color_orange">Finish ></h4>
        </div>
        <div v-else class="display_flex">
          <h3 class="step  color_white bg_color_peach">{{ s }}</h3>
          <h4 v-if="s === 1" class="step__step_details color_orange">Delivery ></h4>
          <h4 v-if="s === 2" class="step__step_details color_orange">Payment ></h4>
          <h4 v-if="s === 3" class="step__step_details color_orange">Finish ></h4>
        </div>
      </div>
    </div>
    <div class="container bg_color_white">
      <form @submit.prevent="handleSubmit" class="checkout-form">
        <div class="row">
          <div class="col-8">
          </div>
          <div class="col-4">
          </div>
        </div>
        <div class="grid-container">
          <div class="container_content">
            <div v-if="currentStep === 1">
              <div class="title__container color_orange pl-3">
                <div>
                  <h1>Delivery Details</h1>
                </div>

                <div class="checkbox__dropshipper">
                  <input class="dropshipper checkbox__dropshipper__checkbox_color" type="checkbox" id="mike"
                    value="Mike" v-model="isDropshipper">
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
            </div>
            <div v-if="currentStep === 2">
              <div class="title__container color_orange pl-3">
                <div>
                  <h1>Shipment</h1>
                </div>
              </div>
              <div class="grid-container__content">
                <div>
                  <div class="display_flex">
                    <SelectedComponent :class="selectedBox === i.name ? 'selected' : 'not-selected'"
                      @click="setValue(i.name)" v-for="i in listBox" v-model:msg="i.name" v-bind:key="i"
                      v-model:price="i.price" />
                  </div>
                </div>
              </div>
              <div class="title__container color_orange pl-3">
                <div>
                  <h1>Payment</h1>
                </div>
              </div>
              <div class="grid-container__content">
                <div>
                  <div class="display_flex">
                    <SelectedComponent :class="selectedBoxPayment === i.name ? 'selected' : 'not-selected'"
                      @click="setValuePayment(i.name)" v-for="i in listBoxPayment" v-model:msg="i.name"
                      v-bind:key="i" />
                  </div>
                </div>
              </div>
            </div>
            <div v-if="currentStep === 3">
              <div class="title__container color_orange pl-3">
                <div>
                  <h1>Thankyou</h1>
                  <h1>Order ID {{ makeRandomString2 }}</h1>
                  <P>Your order will be delivered today with {{ shipping }}</P>
                  <div @click="backToHome()">
                    <p>
                      {{ '<- Go Back to HomePage' }} </p>
                  </div>
                </div>
              </div>
            </div>

          </div>
          <div class="container__summary">
            <div class="container__summary_summary">
              <h3 class="summary color_orange">Summary</h3>
              <p>
                10 Items purchased
              </p>
            </div>

            <div class="display_flex space_between pr-2">
              <p>
                Cost of Goods
              </p>
              <p>
                <b>500,000</b>
              </p>
            </div>

            <div v-if="isDropshipper" class="display_flex space_between pr-2">
              <p>
                Dropshipping Fee
              </p>
              <p>
                <b>5,900</b>
              </p>
            </div>
            <div class="display_flex space_between pr-2 color_orange">
              <h2>
                Total
              </h2>
              <h2>
                {{ isDropshipper? '505,900': '500,000' }}
              </h2>
            </div>
            <div class="address__field ">
              <button type="submit" class="bg_color_orange color_white">Continue to Payment</button>
            </div>
          </div>
        </div>
      </form>
    </div>
  </div>
</template>

<script>

import { reactive } from "vue";
import CustomInput from "./components/CustomInput.vue";
import SelectedComponent from "./components/SelectedComponent.vue";
export default {
  name: "CheckoutForm",
  data: function () {
    return {
      step: 3,
      currentStep: 1,
      isDropshipper: false,
      shippingFee: '500,000',
      shipping: 'GO-SEND',
      payment: 'E-Wallet',
      selectedBox: '',
      selectedBoxPayment: '',
      listBox: [
        {
          name: "GO-SEND",
          price: 15000
        },
        {
          name: "JNE",
          price: 9000
        },
        {
          name: "Personal Courier",
          price: 29000
        },
      ],
      listBoxPayment: [
        {
          name: "E-Wallet",
          // price: 10000
        },
        {
          name: "Bank Transfer",
          // price: 20000
        },
        {
          name: "Virtual Account",
          // price: 30000
        },
      ],
    };
  },
  components: {
    CustomInput,
    SelectedComponent
  },
  methods: {
    handleSubmit() {
      this.currentStep += 1;
    },
    backToHome() {
      this.currentStep = 1;
    },
    setValue(val) {
      this.selectedBox = val;
    },
    setValuePayment(val) {
      this.shipping = val;
      this.selectedBoxPayment = val;
    }
  },
  computed: {
    makeRandomString2() {
      let text = "";
      const possible =
        "ABCDEFGHJKLMNPQRSTUVWXYZ23456789";
      for (let i = 0; i < 5; i++)
        text += possible.charAt(Math.floor(Math.random() * possible.length));
     
      return text;
    },
  },
  setup() {
    const form = reactive({
      dropshipperName: "",
      email: "",
      phone: "",
      deliveryAddress: "",
      dropshipperPhone: "",
    });
    return {
      form,
    };
  },
};
</script>
<style lang="scss">
@import "./components/utility/main.scss";
</style>
