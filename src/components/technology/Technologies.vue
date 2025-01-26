<script setup lang='ts'>
import TechPagination from './TechPagination.vue';
import { ref } from 'vue';

const selectedTech = ref(0);

const techs = [
    {
        title: "Launch vehicle",
        description: "A launch vehicle or carrier rocket is a rocket-propelled vehicle used to carry a payload from Earth's surface to space, usually to Earth orbit or beyond. Our WEB-X carrier rocket is the most powerful in operation. Standing 150 metres tall, it's quite an awe-inspiring sight on the launch pad!",
        image: "launch-vehicle.png"
    },
    {
        title: "Spaceport",
        description: "A spaceport or cosmodrome is a site for launching (or receiving) spacecraft, by analogy to the seaport for ships or airport for aircraft. Based in the famous Cape Canaveral, our spaceport is ideally situated to take advantage of the Earth’s rotation for launch.",
        image: "spaceport.png"
    },
    {
        title: "Space capsule",
        description: "A space capsule is an often-crewed spacecraft that uses a blunt-body reentry capsule to reenter the Earth's atmosphere without wings. Our capsule is where you'll spend your time during the flight. It includes a space gym, cinema, and plenty of other activities to keep you entertained.",
        image: "space-capsule.png"
    }
];

const handleTechSelected = (index: number) => {
    selectedTech.value = index;
}
</script>

<template>
    <div class="tech-wrapper">
        <div class="tech-wrapper__left-pan">
            <TechPagination :techs="techs" @tech-selected="handleTechSelected" />

            <div class="left-pan__introduction">
                <h3 class="text-preset-4">La terminologie...</h3>
                <h2 class="text-preset-3">{{ techs[selectedTech].title }}</h2>
                <p class="text-preset-9">{{ techs[selectedTech].description }}</p>
            </div>
        </div>

        <div class="tech-wrapper__right-pan">
            <div class="tech-image bg-image-1" :class="{ active: selectedTech === 0 }"></div>
            <div class="tech-image bg-image-2" :class="{ active: selectedTech === 1 }"></div>
            <div class="tech-image bg-image-3" :class="{ active: selectedTech === 2 }"></div>
        </div>

    </div>
</template>

<style scoped>
    .tech-wrapper {
        display: flex;
        align-items: center;
        justify-content: space-between;
        padding: var(--spacing-400) 0;
        gap: var(--spacing-400);
    }

    .tech-wrapper__left-pan {
        display: flex;
        align-items: center;
        gap: var(--spacing-400);
        width: 50%;
        padding: var(--spacing-800) 0;
    }

    .left-pan__introduction h3,
    .left-pan__introduction h2 {
        text-transform: uppercase;
        margin: 0;
    }
    .left-pan__introduction h3 {
        opacity: 0.5;
    }
    .left-pan__introduction h2 {   
        margin: var(--spacing-200) 0 var(--spacing-100) 0;
    }

    .tech-wrapper__right-pan {
        position: relative;
        width: 50%;
        height: 75vh;
    }

    .tech-image {
        position: absolute;
        bottom: 0;
        right: 0;
        width: 100%;
        height: 100%;
        opacity: 0;
        background-position: right;
        background-size:contain;
        transition: all 0.3s ease-in-out;
    }
    .tech-image.active {
        opacity: 1;
    }
    .tech-image.bg-image-1 {
        background-image: url("../../assets/techs/launch-vehicle.png");
        background-repeat: no-repeat;
        z-index: 0;
    }
    .tech-image.bg-image-2 {
        background-image: url("../../assets/techs/spaceport.png");
        background-repeat: no-repeat;
        z-index: 5;
    }
    .tech-image.bg-image-3 {
        background-image: url("../../assets/techs/space-capsule.png");
        background-repeat: no-repeat;
        z-index: 10;
    }
</style>