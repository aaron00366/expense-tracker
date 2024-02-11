<template>
    <div class="inc-exp-container">
    <div>
      <h4>入帳</h4>
      <p id="money-plus" class="money plus">+$ {{ income }}</p>
    </div>
    <div>
      <h4>支出</h4>
      <p id="money-minus" class="money minus">$ {{ expense }}</p>
    </div>
  </div>
</template>

<script setup>
import { defineProps } from 'vue';
const props = defineProps({
  income:{
    type:Number,
    required:true
  },
  expense:{
    type:Number,
    required:true
  }
})
</script>