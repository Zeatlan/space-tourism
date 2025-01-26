<script setup lang='ts'>
import { ref, onMounted, watch } from 'vue';

const props = defineProps({
    menu: Array<Object>,
});

const activeMenu = ref("Accueil");

const formattedIndex = (index: number): string => {
    return "0" + index;
}

const handleClick = (item: String) => {
    activeMenu.value = item;
};

const setActiveIndexFromURL = () => {
    const currentURL = window.location.pathname;
    const matchingID = props.menu!.find(item => item.href === currentURL);

    if(matchingID !== -1) {
        activeMenu.value = matchingID.name;
    }
};

onMounted(() => {
    setActiveIndexFromURL();
});
</script>

<template>
    <nav aria-label="Main navigation">
        <div class="left-pan">
           <a href="/"><img src="/assets/Logo.png" alt="Logo"/></a>

            <div class="line">&nbsp;</div>
        </div>

        <ul class="menu">
            <li v-for="(item, index) in menu" :key="index" :class="{ active: item.name === activeMenu }" @click="handleClick(item.name)">
                <a class="text-preset-8" :href="item.href"><span>{{ formattedIndex(index) }}</span> {{ item.name }}</a>
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
    position: relative;
    padding: var(--spacing-200) 0;
    cursor: pointer;
    list-style-type: none;
    transition: all 0.3s ease-in-out;
}

ul.menu li::before {
    content: "";
    position: absolute;
    bottom: 0;
    left: 0;
    width: 100%;
    height: 4px;
    background: var(--blue-300);
    opacity: 0;
    transition: all 0.3s ease-in-out;
}

ul.menu li:hover:not(li.active)::before {
    opacity: 0.7;
}

ul.menu li.active::after {
    content: "";
    position: absolute;
    bottom: 0;
    left: 0;
    width: 100%;
    height: 4px;
    background: var(--blue-300);
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