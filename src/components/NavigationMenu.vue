<script setup lang='ts'>
import { ref } from 'vue';

defineProps({
    menu: Array<String>,
});

const activeIndex = ref(0);

const formattedIndex = (index: number): string => {
    return "0" + index;
}

const handleClick = (index: number) => {
    activeIndex.value = index;
};
</script>

<template>
    <nav aria-label="Main navigation">
        <div class="left-pan">
            <img src="/assets/Logo.png" alt="Logo"/>

            <div class="line">&nbsp;</div>
        </div>

        <ul class="menu">
            <li v-for="(item, index) in menu" :key="index" :class="{ active: index === activeIndex }" @click="handleClick(index)">
                <a class="text-preset-8" href="#"><span>{{ formattedIndex(index) }}</span> {{ item }}</a>
            </li>
        </ul>
    </nav>
</template>

<style>
nav {
    position: relative;
    display: flex;
    align-items: center;
    padding: 40px 0 0 0;
}

nav .left-pan {
    position: absolute;
    display: flex;
    align-items: center;
    width: 50%;
    padding-left: var(--spacing-400);
    z-index: 10;
    gap: var(--spacing-400);
}

nav .left-pan .line {
    width: 100%;
    height: 1px;
    background: var(--white);
    opacity: 0.25;
}

ul.menu {
    display: flex;
    flex-direction: row;
    gap: var(--spacing-300);

    width: 50%;
    justify-content: center;
    align-items: center;
    margin: 0 0 0 auto;

    background: rgba(255, 255, 255, 0.05);
    backdrop-filter: blur(80px);
}

ul.menu li {
    padding: var(--spacing-200) 0;
    cursor: pointer;
    list-style-type: none;
}

ul.menu li.active {
    border-bottom: 2px solid var(--blue-300);
}

ul.menu li a {
    display: flex;
    gap: 12px;
    text-decoration: none;
    color: var(--white);
    text-transform: uppercase;
}

ul.menu li a span {
    font-weight: bold;
}
</style>