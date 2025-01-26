<script setup lang='ts'>
import { ref } from 'vue';

const props = defineProps({
    crews: Array<Object>,
});

const emit = defineEmits(['crew-selected']);

const activeIndex = ref(0);

const clickHandler = (index: number) => {
    activeIndex.value = index;
    emit('crew-selected', index);
}
</script>

<template>
    <ul class="crew-pagination">
        <li v-for="(item, index) in crews" :key="index" class="tab-menu-item" :class="{ active: index === activeIndex }" @click="clickHandler(index)"></li>
    </ul>
</template>

<style scoped>
ul {
    width: 100%;
    margin: 0;
    padding: 0;
    list-style-type: none;
    display: flex;
    align-items: center;
    gap: var(--spacing-400);
}

.tab-menu-item {
    width: 15px;
    height: 15px;
    background: var(--white);
    opacity: 0.25;
    border-radius: 100px;
    cursor: pointer;
    transition: all 0.3s ease-in-out;
}
.tab-menu-item.active {
    opacity: 1;
}
.tab-menu-item:not(.active):hover {
    opacity: 0.5;
}

@media screen and (max-width: 1100px) {
    ul {
        gap: var(--spacing-200);
    }
    .tab-menu-item {
        width: 10px;
        height: 10px;
    }
}
</style>