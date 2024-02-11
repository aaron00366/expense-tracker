<template>
  <div class="container">
    <Header></Header>
    <Balance :total="+total"></Balance>
    <IncomExpense :income="+income" :expense="+expense"></IncomExpense>
    <TransactionList :transactions="transactions" @transctionDeleted="handleTransctionDeletd"></TransactionList>
    <AddTransaction @transcationSubmitted="handleTransctionSubmitted"></AddTransaction>
  </div>
</template>

<script setup>
import Header from './components/Header.vue'
import Balance from './components/Balance.vue'
import IncomExpense from './components/IncomeExpense.vue'
import TransactionList from './components/TransactionList.vue'
import AddTransaction from './components/AddTransaction.vue'
import { ref,computed,onMounted } from 'vue'
import { useToast } from 'vue-toastification'
const toast = useToast()
const transactions = ref([])

onMounted(()=>{
  const savedTranscations = JSON.parse(localStorage.getItem('transactions'))
  if(savedTranscations){
    transactions.value = savedTranscations
  }
})
// Get total
const total = computed(()=>{
  return transactions.value.reduce((acc, transaction)=>{
    return acc + transaction.amount
  },0)
  })
// get income
const income = computed(()=>{
  return transactions.value
  .filter((transaction)=>transaction.amount > 0)
  .reduce((acc, transaction)=>{
    return acc + transaction.amount
  },0)
  .toFixed(2)
  })
// get expense
const expense = computed(()=>{
  return transactions.value
  .filter((transaction)=>transaction.amount < 0)
  .reduce((acc, transaction)=>{
    return acc + transaction.amount
  },0)
  .toFixed(2)
  })

  //add transaction
  const handleTransctionSubmitted = (transcationData)=>{
    transactions.value.push({
      id: generateUniqueId(),
      text: transcationData.text,
      amount: transcationData.amount
    })
    saveTransactionToLocalStorage()
    toast.success('交易紀錄新增成功')
  }

  //generate Unique Id
  const generateUniqueId = ()=>{
    return Math.floor(Math.random() * 1000000000)
  }

  //delete transaction
  const handleTransctionDeletd = (id)=>{
    transactions.value = transactions.value.filter((transaction) =>{
      return transaction.id !== id
    })
    saveTransactionToLocalStorage()
    toast.success('交易紀錄刪除成功')
  }

//sve to local storage
const saveTransactionToLocalStorage = ()=>{
  localStorage.setItem('transactions',JSON.stringify(transactions.value))
}
</script>