<template>
  <div class="clicker-window" @click="eventChecker">
    <img src="@/assets/donut.png" alt="donut" class="donut-img" @click="action" />
    <slot></slot>
    <div class="text" id="text">Donuts:
      <br><text class="points" id="counter" ref="donuts">{{ props.counter }}</text>
    </div>
  </div>
</template>

<script setup>
import { defineEmits, defineProps } from 'vue';
const props = defineProps({
  counter: Number
})
const emit = defineEmits(['click'])
const action = (e) => emit('click', e)

</script>

<style>
.donut-img {
  width: 351px;
  height: 340px;

  margin-left: 61px;
}

/* .donut-img:active {
  animation: fadeInDown;
  animation-duration: 0.5s;
} */

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
</style>