<template>
    <div class="clearAllContainer">
        <span class="clearAllBtn" v-on:click="clearTodo">Clear All</span>
    </div>
</template>
<script setup>
import { defineEmits } from 'vue';

const emit = defineEmits(['clearAll']);

const clearTodo = () => {
    emit('clearAll');
}
</script>

<style scoped>
.clearAllContainer {
    width: 8.5rem;
    height: 50px;
    line-height: 50px;
    background-color: white;
    border-radius: 5px;
    margin: 0 auto;
}

.clearAllBtn {
    color: #e20404;
    display: block;
}
</style>