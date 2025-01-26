<script setup lang='ts'>
import { ref } from 'vue';

const props = defineProps({
    techs: Array<Object>,
});

const emit = defineEmits(['tech-selected']);

const activeIndex = ref(0);

const clickHandler = (index: number) => {
    activeIndex.value = index;
    emit('tech-selected', index);
}

</script>

<template>
    <ul>
        <li v-for="(item, index) in techs" :key="index" class="tab-menu-item" :class="{ active: index === activeIndex }" @click="clickHandler(index)">
            <span class="text-preset-4">{{ index+1 }}</span>
        </li>
    </ul>
</template>

<style scoped>
ul {
    list-style-type: none;
    margin: 0;
    padding: 0;
    display: flex;
    flex-direction: column;
    gap: var(--spacing-200);
}

.tab-menu-item {
    width: 80px;
    height: 80px;
    display: flex;
    align-items: center;
    justify-content: center;
    color: var(--white);
    border-radius: 100%;
    border: 1px solid rgba(255, 255, 255, 0.25);
    cursor: pointer;
    transition: all 0.3s ease-in-out;
}
.tab-menu-item:not(.active):hover {
    border: 1px solid var(--white);
}
.tab-menu-item.active {
    color: var(--blue-900);
    background: var(--white);
}
</style>