<script setup lang='ts'>
const props = defineProps({
    menu: Array<Object>,
    activeMenu: String,
    isBurgerOpen: Boolean,
});

const emit = defineEmits(['menu-selected', 'hide-menu']);

const formattedIndex = (index: number): string => {
    return "0" + index;
}

const hideMenu = () => {
    emit('hide-menu', true);
}

const handleClick = (item: String) => {
    emit('menu-selected', item);
    hideMenu();
}
</script>

<template>
    <div class="mobile-navigation" :class="{ open: isBurgerOpen }">
        <div class="act-btn">
            <div class="close-button" @click="hideMenu"></div>
        </div>

        <ul class="menu">
            <a v-for="(item, index) in menu" :key="index" class="text-preset-8" :href="item.href">
                <li :class="{ active: item.name === activeMenu }" @click="handleClick(item.name)">
                    <span>{{ formattedIndex(index) }}</span> {{ item.name }}
                </li>
            </a>
        </ul>
    </div>
</template>

<style scoped>
.mobile-navigation {
    display: none;
}

.menu {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    height: 100%;
    list-style-type: none;
    gap: var(--spacing-300);
}

.menu a {
    text-decoration: none;
    color: rgba(255, 255, 255, 0.8);
    font-size: 48px;
}

.menu span {
    font-weight: 700;
    color: rgba(255, 255, 255, 1);
}

.act-btn {
    position: absolute;
    right: 0;
    display: flex;
    justify-content: end;
    margin: var(--spacing-300);
}

.close-button {
    background: var(--white);
    width: 48px;
    height: 3px;
    position: absolute;
    top: 0;
    background: transparent;
}

.close-button::after,
.close-button::before {
    content: "";
    background: var(--white);
    width: 48px;
    height: 3px;
    position: absolute;
    top: 0;
}
.close-button::after {
    transform: rotate(45deg);
}
.close-button::before {
    transform: rotate(-45deg);
}

@media screen and (max-width: 768px) {
    .mobile-navigation {
        display: block;
        position: fixed;
        top: 0;
        left: 100%;
        width: 100%;
        height: 100%;
        background: var(--blue-900);
        backdrop-filter: blur(80px);
        z-index: 100;
        transition: all 0.3s cubic-bezier(0.6, -0.28, 0.735, 0.045);
    }

    .mobile-navigation.open {
        left: 0;
    }
}
</style>