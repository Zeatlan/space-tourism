<script setup lang='ts'>
import { ref } from 'vue';

defineProps({
    menu: Array<String>,
})

const emit = defineEmits(['planet-selected'])

const activeIndex = ref(0);

const clickHandler = (index: number) => {
    activeIndex.value = index;
    emit('planet-selected', index);
};
</script>

<template>
    <ul class="tab-menu">
        <li v-for="(item, index) in menu" :key="index" class="tab-menu-item" :class="{ active: index === activeIndex }" @click="clickHandler(index)">
            {{ item }}
        </li>
    </ul>
</template>

<style scoped>
ul.tab-menu {
    display: flex;
    align-items: center;
    list-style-type: none;
    text-transform: uppercase;
    gap: var(--spacing-200);
    padding: 0;
}
ul.tab-menu li {
    position: relative;
    color: var(--blue-300);
    padding-bottom: var(--spacing-100);
    cursor: pointer;
    transition: all 0.3s ease-in-out;
}

ul.tab-menu li.active {
    color: var(--white);
}
ul.tab-menu li::after,
ul.tab-menu li.active::after {
    content: "";
    position: absolute;
    bottom: 0;
    left: 0;
    width: 100%;
    height: 3px;
    background: var(--white);
    transition: all 0.3s ease-in-out;
    z-index: -1;
}
ul.tab-menu li::after {
    opacity: 0;
}
ul.tab-menu li.active::after {
    opacity: 1;
}

ul.tab-menu li:hover {
    color: var(--white);
}
ul.tab-menu li:not(li.active):hover::after {
    opacity: 0.5;
}
</style>