<template>
    <h3>新增交易紀錄</h3>
    <form id="form" @submit.prevent="onSubmit">
      <div class="form-control">
        <label for="text">交易品項</label>
        <input type="text" id="text" placeholder="輸入文字..." v-model="text" />
      </div>
      <div class="form-control">
        <label for="amount"
          >交易金額 <br />
          ( (-) - 支出, (+) - 入帳)</label
        >
        <input
          type="text"
          id="amount"
          placeholder="確認金額..." v-model="amount"
        />
      </div>
      <button class="btn">新增交易紀錄</button>
    </form>
  </template>

  <script setup>
import { ref } from 'vue';
import {useToast} from 'vue-toastification'
const toast = useToast()
const text = ref('');
const amount = ref('');
const emit = defineEmits(['transcationSubmitted'])
const onSubmit = ()=>{
  if(!text.value || !amount.value ){
    toast.error('請輸入交易品項和金額')
    return;
  }
  
  const transcationData = {
    text:text.value,
    amount: parseFloat(amount.value)
  }
  emit('transcationSubmitted', transcationData)
  text.value = ''
  amount.value = ''
}
</script>