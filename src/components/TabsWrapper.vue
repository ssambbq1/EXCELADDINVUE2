<template>
    <div class="tabs">
        <ul class="tabs__header">
            <li 
            v-for="title in tabTitles"
             :key="title"
             :class="{ selected: title == selectedTitle}"
             @click="selectedTitle = title"
             >
            {{ title }}
        </li>
        </ul>
       <slot />
    </div>
</template>

<script>
import {ref, provide} from 'vue'
export default {
   setup(props, {slots}) {
    const tabTitles = ref(slots.default().map((tab) => tab.props.title))
    const selectedTitle = ref(tabTitles.value[0])

    provide("selectedTitle", selectedTitle)  
    return {
        selectedTitle,
        tabTitles,
    }
   },
    }
</script>

<style scoped>
.tabs {
    max-width: 100%;
    margin: 0 auto;
}

.tabs__header{
    margin-bottom: 10px;
    list-style: none;
    padding: 0;
    display: flex;
    font-size:15px;
}

.tabs__header li {
    width: 25%;
    text-align: center;
    padding: 5px 10px;
    margin-right: 5px;
    background-color: #ddd;
    border-radius: 5px;
    cursor: pointer;
    transition: 0.4s all ease-out;
}

.tabs__header li.selected {
    background-color: #0984e3;
    color: white;
}
</style>