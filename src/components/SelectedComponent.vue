<template>
    <div class="box pointer" @click="setValue()">
        <div >
            <p >
                {{ msg }}
            </p>
        </div>
        <div>
            <p>
                {{ price }}
            </p>
        </div>

    </div>
</template>

<script>
import { formatPrice } from './utils';

export default {
    name: 'SelectedComponent',
    props: {
        msg: String,
        price: Number,
    },
    methods: {
        setValue(){
            this.$emit('action2','🦄')
            console.log("ss");
        }
        // price(){
        //     formatPrice
        // }
    },
    watch: {
        price() {
            return formatPrice(this.price);
        }
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.box {
    width: 10vw;
    height: 11vh;
    max-height: 100px;
    max-width: 150px;
    border: solid 1px grey;
    text-align: left;
    padding-left: 1vw;
    margin-left: 1.5vw;
}
.pointer {cursor: pointer;}
</style>
