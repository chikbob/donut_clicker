<template>
    <button :disabled="isEnabled == false" class="donutBronze" @click="buyBuff">
        <img :src="require(`@/assets/${props.imgButton}`)" width="68" height="68">
        <div v-if="props.coefficientBuff > props.coefficientApp" class="text_price_donut_bronze" id="text_price_donut_bronze">
            <text class="price-donut-bronze" id="price-donut-bronze">{{ price }}</text>
            <img class="price-donut-bronze_img" src="@/assets/donut.png" width="32" height="32">
        </div>
        <div v-if="props.coefficientBuff > props.coefficientApp" class="help_coefficient_donutBronze" width="68" height="68">
            <text id="help_coefficient_donutBronze">{{ "x"+props.coefficientBuff }}</text>
        </div>
        <div v-else>
            <div class="Sold">SOLD</div>
        </div>
    </button>
</template>

<script setup>
import { ref, defineProps, defineEmits, computed } from 'vue'

const props = defineProps({
    priority: Number,
    coefficientApp: Number,
    counter: Number,
    imgButton: String,
    coefficientBuff: Number,
    startCost: Number,
    buy: Boolean
})

let price = ref(props.startCost)
let solded = ref(props.buy)
console.log(solded.value)

let emits = defineEmits(['onBuyBuff'])

const isEnabled = computed(() => props.coefficientBuff > props.coefficientApp)

function buyBuff() {
    if (price.value > props.counter) {
        return false
    }
    console.log(props.coefficientApp + " " + props.coefficientBuff)
    solded.value = true
    let oldPrice = price.value
    console.log(solded.value + " " + props.coefficientApp + " " + props.coefficientBuff)
    emits('onBuyBuff', oldPrice, props.coefficientBuff)
}

</script>

<style lang="scss" scoped>
.donutBronze {
    width: 110px;
    height: 114px;

    display: flex;
    flex-direction: column;
    justify-content: center;

    align-items: center;

    background: #D96A9F;
    border: 2px solid #59002B;

    cursor: pointer;
}

.text_price_donut_bronze {
    height: 32px;

    display: flex;

    justify-content: center;
    align-items: center;
}

.price-donut-bronze_img {
    display: flex;
    margin: auto
}

.price-donut-bronze {
    width: 70%;
    height: 22px;

    display: flex;
    justify-content: center;

    font-family: 'Henny Penny';
    font-style: normal;
    font-weight: 400;
    font-size: 20px;
    line-height: 35px;
    text-align: end;
    margin: auto;

    color: #59002B;
}

.help_coefficient_donutBronze {
    display: none;
}

.help_coefficient_donutBronze text {
    display: flex;

    font-family: 'Henny Penny';
    font-style: normal;
    font-weight: 400;
    font-size: 20px;
    line-height: 35px;

    color: #59002B;
    align-items: flex-end;
    justify-content: center;

    margin-bottom: -60px;
}

.Sold {
    height: 22px;
    padding-top: 10px;

    font-family: 'Henny Penny';
    font-style: normal;
    font-weight: 400;
    font-size: 20px;
    display: flex;
    align-items: center;
    text-align: center;

    flex-direction: row;

    color: #59002B;
}

.donutBronze:hover .help_coefficient_donutBronze {
    display: flex;
}
</style>