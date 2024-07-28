<script lang="ts" setup>
import { defineProps, defineEmits } from 'vue';
defineProps<{
    isChecked: boolean | false
}>()

const emit = defineEmits(['update'])

const handleClick = () => {
    emit('update')
}
</script>
<template>
    <label :class="{ 'checked': isChecked }" @click="handleClick">
        <input type="checkbox" :checked="isChecked"/>
        <slot></slot>
    </label>
</template>

<style scoped>
label {
   cursor: pointer;
}
.checked {
    text-decoration: line-through;
}
</style>