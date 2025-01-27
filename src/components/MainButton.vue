<script setup lang='ts'>
defineProps({
    baseUrl: String,
})
</script>

<template>
    <a :href="`${baseUrl}/destination`" class="main-button">
        <span class="text-preset-4"><slot /></span>
    </a>
</template>

<style>
.main-button {
    position: relative;
    background: var(--white);
    border-radius: 100%;
    width: 272px;
    height: 272px;
    display: flex;
    align-items: center;
    justify-content: center;
    cursor: pointer;
    text-decoration: none;
    color: var(--blue-900);
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

@media screen and (max-width: 768px) {
    .main-button {
        width: 180px;
        height: 180px;
    }
}
</style>