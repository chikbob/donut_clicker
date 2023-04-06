<template>
    <button class="btn" @click="buyNewClick">
        <img src="@/assets/clicker.png" width="68" height="68">
        <div class="name_and_price"><text class="name">{{ props.nameButton }}</text>
            <div class="for_donut">
                <img src="@/assets/donut.png" width="32" height="32">
                <text class="price_donut" id="price_donut">{{ price_click_num }}</text>
            </div>
        </div>
        <text class="count_donut" id="count_donut">{{ count_click_num }}</text>
    </button>
</template>

<script setup>
import { ref, defineProps, defineEmits } from 'vue'

// $attrs['counter']
let price_click_num = ref(200)
let count_click_num = ref(0)

const props = defineProps({
    counter: Number,
    nameButton: String
})

let emits = defineEmits(['onBuyNewDonut'])


function buyNewClick() {
    if (price_click_num.value > props.counter) {
        return false
    }
    count_click_num.value += 1
    let oldPrice = price_click_num.value
    price_click_num.value = Math.floor((price_click_num.value + 15) * 1.3)
    emits('onBuyNewDonut', count_click_num.value, oldPrice)
    console.log(count_click_num.value)
}
</script>

<style lang="scss" scoped>
.btn {
    display: flex;
    align-items: center;

    width: 370px;
    height: 114px;
    margin-top: 62px;

    margin-left: 67px;

    background: #D96A9F;
    border: 2px solid #59002B;

    cursor: pointer;
}

.btn img {
    transform: matrix(0.85, 0.53, -0.4, 0.92, 0, 0);
}

.name_and_price {
    display: flex;
    flex-direction: column;
}

button img {
    margin-left: 16px;
}

.for_donut {
    display: flex;
    align-items: center;
    flex-direction: row;

}

.price_donut {
    width: 61px;
    height: 26px;

    display: flex;

    font-family: 'Henny Penny';
    font-style: normal;
    font-weight: 400;
    font-size: 20px;
    line-height: 35px;

    color: #59002B;
    align-items: flex-start;
    justify-content: flex-start;

    margin-left: 6px;
}

.name {
    display: flex;
    width: 217px;
    height: 50px;

    margin-left: 16px;
    margin-bottom: 6px;

    font-family: 'Henny Penny';
    font-style: normal;
    font-weight: 400;
    font-size: 40px;
    line-height: 71px;

    color: #59002B;
}

.count_donut,
.count_package,
.count_bar,
.count_click {
    width: 44px;
    height: 88px;
    font-family: 'Henny Penny';
    font-style: normal;
    font-weight: 400;
    font-size: 40px;
    line-height: 71px;
    display: flex;
    align-items: flex-end;
    text-align: center;

    margin-right: 10px;

    flex-direction: row;
    justify-content: flex-end;

    color: #59002B;
}
</style>