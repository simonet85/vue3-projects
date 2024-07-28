<script setup lang="ts">
    import { ref, computed, onMounted } from 'vue';
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
            setToStorage(storageItems.value)
        }
    }
    const findItemInList = (item: Item): Item | undefined => {
        return storageItems.value.find((itemInList: Item) => itemInList.title === item.title)
    }
    const toggleItemChecked = (item: Item): void  => {
        item.checked = !item.checked
    }

    const sortedList = computed(() => {
        return [...storageItems.value].sort((a, b) => (a.checked ? 1 : 0) - (b.checked ? 1 : 0));
    });
    const setToStorage = (items: Item[]) => {
        localStorage.setItem('list-items', JSON.stringify(items))
    }

    const getFromStorage = (): Item[] => {
        const stored = localStorage.getItem('list-items')
        if(stored) {
            return JSON.parse(stored)
        }
        return []
    }

    const storageItems: Ref<Item[]> = ref(getFromStorage())

    const initListItems = ():void => {
            if(storageItems.value?.length===0) {
                const listItems = [
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
        ]
        setToStorage(listItems)
        storageItems.value = listItems
        }
    }
    onMounted(() => {
        initListItems()
        storageItems.value = getFromStorage()
    })
</script>
<template>
    <ul>
        <li v-for="(item, key) in sortedList" :key="key">
            <ListItem v-if="item.checked !== undefined" :is-checked="item.checked" @update="updateItem(item)">{{ item.title }}</ListItem>
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