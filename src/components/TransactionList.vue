<template>
    <h3>交易紀錄</h3>
    <ul class="list" id="list">
        <li v-for="transaction in transactions" :key="transaction.id" :class="transaction.amount < 0 ? 'minus' : 'plus'">
            {{transaction.text}} 
            <span>$ {{ transaction.amount }}</span>
        <button class="delete-btn" @click="deleteTransction(transaction.id)">x</button>
        </li>
    </ul>
</template>
<script setup>
import { defineProps } from 'vue';
const emit = defineEmits(['transctionDeleted'])
const props = defineProps({
    transactions: {
        type: Array,
        required: true
    },
})
const deleteTransction = (id) =>{
    emit('transctionDeleted', id)
}
</script>