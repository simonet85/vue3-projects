<script setup lang="ts">
    import { ref } from 'vue';
    import type { Ref } from 'vue';
    import ListItem from './ListItem.vue';
    type Item = {
        title: string,
        checked?: boolean
    };
    const listItems: Ref<Item[]> = ref([
        {
            title: 'Make a todo list app',
            checked: true
        },
        {
            title: 'Predict the weather',
            checked: false
        },
        {
            title: 'Play some tunes',
            checked: false
        },
        {
            title: 'Get some sleep',
            checked: false
        },
        {
            title: 'Pump some iron',
            checked: false
        },
        {
            title: 'Have some fun',
            checked: false
        },
        {
            title: 'Track my expenses',
            checked: false
        },
        {
            title: 'Have some fun wit kids',
            checked: false
        }
    ]);
    const updateItem = (item: Item ):void =>{
        const updatedItem = findItemInList(item)
        if (updatedItem) {
            toggleItemChecked(updatedItem)
        }
    }
    const findItemInList = (item: Item): Item | undefined => {
        return listItems.value.find((itemInList: Item) => itemInList.title === item.title)
    }
    const toggleItemChecked = (item: Item): void  => {
        item.checked = !item.checked
    }
</script>
<template>
    <ul>
        <li v-for="(item, key) in listItems" :key="key">
            <ListItem :is-checked="item.checked" @update="updateItem(item)">{{ item.title }}</ListItem>
        </li>
    </ul>
</template>

<style scoped>
ul {
    list-style-type: none;
    padding: 0;
}
li{
    margin: 0.4rem 0.2rem;
}
</style>