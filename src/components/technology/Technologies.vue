<script setup lang='ts'>
import TechPagination from './TechPagination.vue';
import { ref } from 'vue';

const selectedTech = ref(0);

const techs = [
    {
        title: "Véhicule de lancement",
        description: "Un véhicule de lancement ou une fusée porteuse est un véhicule propulsé par une fusée utilisé pour transporter une charge utile de la surface de la Terre vers l'espace, généralement vers l'orbite terrestre ou au-delà. Notre fusée porteuse WEB-X est la plus puissante en service. Avec ses 150 mètres de haut, elle est impressionnante sur le pas de tir !",
        image: "launch-vehicle.png"
    },
    {
        title: "Port spatial",
        description: "Un port spatial ou cosmodrome est un site de lancement (ou de réception) d'engins spatiaux, par analogie avec le port maritime pour les navires ou l'aéroport pour les avions. Basé au célèbre Cap Canaveral, notre port spatial est idéalement situé pour profiter de la rotation de la Terre pour le lancement.",
        image: "spaceport.png"
    },
    {
        title: "Capsule Spatiale",
        description: "Une capsule spatiale est un vaisseau spatial souvent doté d'un équipage qui utilise une capsule de rentrée à corps contondant pour rentrer dans l'atmosphère terrestre sans ailes. C'est dans notre capsule que vous passerez votre temps pendant le vol. Elle comprend une salle de gymnastique spatiale, un cinéma et de nombreuses autres activités pour vous divertir.",
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