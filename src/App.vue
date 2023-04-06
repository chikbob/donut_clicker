<template>
  <div class="label">Donut clicker</div>
  <div class="all-content">
    <ClickerWindow
    class="clickerButton"
    @click="generateClick" 
    :disabled="isAnimating"
    :counter="counter"
    >
      <div 
      :style="{ top: y + 'px', left: x + 'px' }" 
      v-show="showAnimation" 
      class="miniAnimation__numberAndIcon"
      >+{{ upgradeCounter+1 }} 
      <img src="@/assets/donut.png" alt="donut" width="30" height="30">
      </div>
    </ClickerWindow>
  <div class="all-donut">
      <div class="donuts_buffsForPerSecond">
        <div class="donut">
          <BuffDonutButton
          class="start"
          :coefficient-app="currentCoefficientBuffDonut"
          :counter="counter"
          img-button='button-donut-bronze.png'
          :coefficient-buff="2"
          :start-cost="400"
          :buy="false"
          @on-buy-buff="upgradePriceMultiplierDonut"
          />
          <BuffDonutButton
          class="midAndEnd"
          :coefficient-app="currentCoefficientBuffDonut"
          :counter="counter"
          img-button='button-donut-silver.png'
          :coefficient-buff="4"
          :start-cost="900"
          :buy="false"
          @on-buy-buff="upgradePriceMultiplierDonut"
          />
          <BuffDonutButton
          class="midAndEnd"
          :coefficient-app="currentCoefficientBuffDonut"
          :counter="counter"
          img-button='button-donut-gold.png'
          :coefficient-buff="8"
          :start-cost="1500"
          :buy="false"
          @on-buy-buff="upgradePriceMultiplierDonut"
          />
        </div>
        <div class="donut packageAndBar">
          <BuffDonutButton
          :coefficient-app="currentCoefficientBuffPackage"
          :counter="counter"
          img-button='donut-box-bronze.png'
          :coefficient-buff="2"
          :start-cost="2000"
          @on-buy-buff="upgradePriceMultiplierPackage"
          />
          <BuffDonutButton
          class="midAndEnd"
          :coefficient-app="currentCoefficientBuffPackage"
          :counter="counter"
          img-button='donut-box-silver.png'
          :coefficient-buff="4"
          :start-cost="3500"
          :buy="false"
          @on-buy-buff="upgradePriceMultiplierPackage"
          />
          <BuffDonutButton
          class="midAndEnd"
          :coefficient-app="currentCoefficientBuffPackage"
          :counter="counter"
          img-button='donut-box-gold.png'
          :coefficient-buff="8"
          :start-cost="5000"
          @on-buy-buff="upgradePriceMultiplierPackage"
          />
        </div>
        <div class="donut packageAndBar">
          <BuffDonutButton
          :coefficient-app="currentCoefficientBuffBar"
          :counter="counter"
          img-button='bar-bronze.png'
          :coefficient-buff="2"
          :start-cost="20000"
          @on-buy-buff="upgradePriceMultiplierBar"
          />
          <BuffDonutButton
          class="midAndEnd"
          :coefficient-app="currentCoefficientBuffBar"
          :counter="counter"
          img-button='bar-silver.png'
          :coefficient-buff="4"
          :start-cost="35000"
          @on-buy-buff="upgradePriceMultiplierBar"
          />
          <BuffDonutButton
          class="midAndEnd"
          :coefficient-app="currentCoefficientBuffBar"
          :counter="counter"
          img-button='bar-gold.png'
          :coefficient-buff="8"
          :start-cost="40000"
          @on-buy-buff="upgradePriceMultiplierBar"
          />
        </div>
      </div>
  </div>
    <div class="perSecond">
      <DonutButton 
      style="margin-top:0 !important;"
      @on-buy-new-donut="onBuyNewDonutHandler" 
      :counter="counter" 
      :interval="2000"
      img-button='button-donut.png'
      :name-button="'Donut'"
      :price-multiplier="1"
      :start-cost="20"
      :current-buff="currentCoefficientBuffDonut"
      @on-tick="onTickHandler"
      />
      <DonutButton
      @on-buy-new-donut="onBuyNewDonutHandler" 
      :counter="counter" 
      :interval="700"
      img-button='donut-box1.png'
      :name-button="'Package'"
      :price-multiplier="1"
      :start-cost="100"
      :current-buff="currentCoefficientBuffPackage"
      @on-tick="onTickHandler"
      />
      <DonutButton
      @on-buy-new-donut="onBuyNewDonutHandler" 
      :counter="counter" 
      :interval="250"
      img-button='bar.png'
      :name-button="'Bar'"
      :price-multiplier="1"
      :start-cost="1000"
      :current-buff="currentCoefficientBuffBar"
      @on-tick="onTickHandler"
      />
      <ClickButton
      :counter="counter" 
      @click="plusOneUpgradeCounter"
      @on-buy-new-donut="onBuyNewDonutHandler" 
      :name-button="'Click'"
      />
    </div>
  </div>
</template> 

<script setup>
import DonutButton from './UI/DonutButton.vue';
import { ref } from 'vue'
import ClickerWindow from './components/ClickerWindow.vue';
import ClickButton from './UI/ClickButton.vue';
import BuffDonutButton from './UI/BuffDonutButton.vue';

const counter = ref(0);
const upgradeCounter = ref(0)
let currentCoefficientBuffDonut = ref(1)
let currentCoefficientBuffPackage = ref(1)
let currentCoefficientBuffBar = ref(1)

const ANIMATION_DURATION = 350

const showAnimation = ref(false)
const isAnimating = ref(false)

let x = ref(0)
let y = ref(0)

function generateClick(e) {
  counter.value += 1 + upgradeCounter.value
  if (isAnimating.value) return // если анимация уже идет, то ничего не делаем
  
  showAnimation.value = true
  isAnimating.value = true

  x = e.clientX
  y = e.clientY

  setTimeout(() => {
    showAnimation.value = false
    isAnimating.value = false
  }, ANIMATION_DURATION)

}
function onBuyNewDonutHandler(toAdd, oldPrice) {
  counter.value -= oldPrice
}
function onTickHandler(toAdd) {
  counter.value += toAdd
}
function plusOneUpgradeCounter() {
  upgradeCounter.value++
}
function upgradePriceMultiplierDonut(oldPrice, coeffOfBuff) {
  counter.value -= oldPrice
  currentCoefficientBuffDonut.value = coeffOfBuff
}
function upgradePriceMultiplierPackage(oldPrice, coeffOfBuff) {
  counter.value -= oldPrice
  currentCoefficientBuffPackage = coeffOfBuff
}
function upgradePriceMultiplierBar(oldPrice, coeffOfBuff) {
  counter.value -= oldPrice
  currentCoefficientBuffBar = coeffOfBuff
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
}
body {
  margin: 0;
  border: 0;
  background-image: url('@/assets/background.webp');
}
.label {
  display: flex;
  justify-content: center;

  margin: auto;
  margin-top: 10px !important;

  width: 337px;
  height: 73px;

  font-family: 'Henny Penny';
  font-style: normal;
  font-weight: 400;
  font-size: 50px;
  line-height: 89px;

  color: #59002B;
}
.miniAnimation__numberAndIcon {
  pointer-events: none;
  position: absolute;
  display: flex;
  align-items: center;
  justify-content: center;
  align-content: center;
  
  animation: zoomIn;
  animation-duration: 0.2s;

  text-align: center;

  font-family: 'Henny Penny';
  font-style: normal;
  font-weight: 400;
  font-size: 30px;
  line-height: 30px;
  text-align: center;

  color: #59002B;
}
.clickerButton img {
  cursor: pointer;
}
.all-content {
  display: flex;
  flex-direction: row;

  width: 100%;
}
.donut-img {
  width: 351px;
  height: 340px;

  margin-left: 61px;
}
.points,
.text {
  text-align: center;

  font-family: 'Henny Penny';
  font-style: normal;
  font-weight: 400;
  font-size: 50px;
  line-height: 89px;
  text-align: center;

  color: #59002B;
}
.text {
  width: 178px;
  height: 178px;

  margin-left: 147px;
}

.all-donut {
    display: flex;
    flex-direction: row;
    justify-content: center;
    margin-left: 86px;
    width: 100%;

    margin-top: 35px;
}
.donut {
  display: flex;
  flex-direction: row;
}
.donuts_buffsForPerSecond {
    display: flex;
    flex-direction: column;

    margin-top: 20px;
}
.midAndEnd {
  margin-left: 60px;
}
.packageAndBar {
  margin-top: 62px
}
.donuts {
    display: flex;
    flex-direction: column;

    margin-left: 40px;

    margin-top: 40px;
}

.perSecond {
    margin-left: 45px;
    display: flex;
    flex-direction: column;
    margin-right: 40px;

    margin-top: -40px;
}
</style>
