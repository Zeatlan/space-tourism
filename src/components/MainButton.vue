<script setup lang='ts'>
</script>

<template>
    <button class="main-button">
        <span class="text-preset-4"><slot /></span>
    </button>
</template>

<style>
.main-button {
    position: relative;
    background: var(--white);
    border-radius: 100%;
    padding: var(--spacing-800) var(--spacing-400);
    cursor: pointer;
    transition: all 0.3s ease-in-out;
}
.main-button::before {
    content: "";
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    border-radius: 100%;
    background: var(--blue-900);
    opacity: 0.5;
    transition: all 0.3s ease-in-out;
    z-index: -1;
}

.main-button:hover {
    color: rgba(11, 13, 23, 0.5);
}

.main-button:hover::before {
    transform: scale(1.5);
}

.main-button span {
    text-transform: uppercase;
}
</style>