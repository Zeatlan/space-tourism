<script setup lang='ts'>
import { ref, onMounted, watch } from 'vue';
import MobileNavigationMenu from './MobileNavigationMenu.vue';

const props = defineProps({
    menu: Array<Object>,
    baseUrl: String,
});

const activeMenu = ref("Accueil");
const isBurgerOpen = ref(false);
const burgerLine = ref(null);

const formattedIndex = (index: number): string => {
    return "0" + index;
}

const handleClick = (item: String) => {
    activeMenu.value = item;
};

const setActiveIndexFromURL = () => {
    const currentURL = window.location.pathname.split("/").filter(Boolean).pop();
    const matchingID = props.menu!.find(item => {
        return item.href.split("/").filter(Boolean).pop() === currentURL
    });

    if(matchingID !== -1) {
        activeMenu.value = matchingID.name;
    }
};

const handleBurger = () => {
    isBurgerOpen.value = !isBurgerOpen.value;

    if(isBurgerOpen.value) {
        burgerLine.value.classList.add("open");
    }else {
        burgerLine.value.classList.remove("open");
    }
}

onMounted(() => {
    setActiveIndexFromURL();
});
</script>

<template>
    <nav aria-label="Main navigation">
        <div class="left-pan">
           <a :href="baseUrl"><img :src="`${baseUrl}/assets/Logo.png`" alt="Logo" class="logo" /></a> 

            <div class="line">&nbsp;</div>
        </div>

        <div class="burger-icon" @click="handleBurger">
            <div class="burger-line" ref="burgerLine"></div>
        </div>

        <ul class="menu">
            <a v-for="(item, index) in menu" :key="index" class="text-preset-8" :href="item.href"><li :class="{ active: item.name === activeMenu }" @click="handleClick(item.name)" >
                <span>{{ formattedIndex(index) }}</span> {{ item.name }}
            </li></a>
        </ul>
    </nav>

    <MobileNavigationMenu :menu="menu" :activeMenu="activeMenu" :isBurgerOpen="isBurgerOpen" @hide-menu="handleBurger" @menu-selected="handleClick" />
</template>

<style scoped>
    nav {
        position: relative;
        display: flex;
        align-items: center;
        padding: 40px 0 0 0;
    }

    .burger-icon {
        position: relative;
        display: none;
        flex-direction: column;
        width: 10%;
        height: 30px;
        justify-content: center;
        gap: 8px;
    }

    .burger-line,
    .burger-line::before,
    .burger-line::after {
        display: block;
        position: absolute;
        transform-origin: center;
        width: 100%;
        height: 3px;
        border-radius: 10px;
        background: var(--white);
        transition: all 0.3s cubic-bezier(0.6, -0.28, 0.735, 0.045);
    }

    .burger-line::before {
        content: "";
        top: -10px;
    }

    .burger-line::after {
        content: "";
        top: 10px;
    }

    .burger-line.open {
        background: transparent;
    }

    .burger-line.open::before {
        top: 0;
        transform: rotate(45deg);
    }

    .burger-line.open::after {
        top: 0;
        transform: rotate(-45deg);
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

    ul.menu a {
        display: flex;
        gap: 12px;
        text-decoration: none;
        color: var(--white);
        text-transform: uppercase;
    }

    ul.menu li a span {
        font-weight: bold;
    }

    @media screen and (max-width: 1100px) {
        nav {
            padding: 0;
        }
        ul.menu {
            width: 65%;
            justify-content: right;
            padding-right: var(--spacing-400)
        }

        .logo {
            width: 48px;
        }
        .line {
            display: none;
        }
	}

    @media screen and (max-width: 768px) {
        nav {
            align-items: center;
            justify-content: space-between;
            padding: var(--spacing-200) var(--spacing-150) 0 var(--spacing-150);
        }
        nav .left-pan {
            position:relative;
            padding-left: 0;
        }
        .burger-icon {
            display: flex;
        }
        ul.menu {
            display: none;
        }
        .line {
            display: none;
        }
    }
</style>