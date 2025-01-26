<script setup lang='ts'>
import PlanetInfo from "./PlanetInfo.vue";
import TabMenu from "./TabMenu.vue";
import { ref, computed } from "vue";

const currentPlanet = ref(0);

const planets = [
    {
        asset: "Moon.png",
        name: "Lune",
        description: "Observez notre planète comme vous ne l'avez jamais vue auparavant. Un voyage de détente idéal pour reprendre du poil de la bête et revenir frais et dispos. Pendant que vous y êtes, faites un peu d'histoire en visitant les sites d'atterrissage de Luna 2 et d'Apollo 11.",
        distance: "384,400 km",
        time: "3 jours",
    },
    {
        asset: "Moon.png",
        name: "Mars",
        description: "N'oubliez pas de prendre vos chaussures de randonnée. Vous en aurez besoin pour vous attaquer au Mont Olympe, la plus haute montagne planétaire de notre système solaire. Elle est deux fois et demie plus grande que l'Everest !",
        distance: "225 mil. km",
        time: "9 mois",
    },
    {
        asset: "Moon.png",
        name: "Europe",
        description: "La plus petite des quatre lunes galiléennes en orbite autour de Jupiter, Europe est un paradis pour les amateurs d'hiver. Avec sa surface glacée, elle est parfaite pour faire du patin à glace, du curling, du hockey ou tout simplement pour se détendre dans son chalet d'hiver douillet.",
        distance: "628 mil. km",
        time: "3 ans",
    },
    {
        asset: "Moon.png",
        name: "Titan",
        description: "La seule lune connue à posséder une atmosphère dense autre que celle de la Terre, Titan est un foyer éloigné du notre (avec quelques centaines de degrés en moins !). En prime, vous aurez une vue imprenable sur les anneaux de Saturne.",
        distance: "1.6 bil. km",
        time: "7 ans",
    },
]

const handlePlanetSelected = (index: number) => {
    currentPlanet.value = index;
};
</script>

<template>
    <div class="planet-container">
        <div class="planet-container__left">
            <div class="planet-img moon" :class="{ active: currentPlanet === 0 }">&nbsp;</div>
            <div class="planet-img mars" :class="{ active: currentPlanet === 1 }">&nbsp;</div>
            <div class="planet-img europa" :class="{ active: currentPlanet === 2 }">&nbsp;</div>
            <div class="planet-img titan" :class="{ active: currentPlanet === 3 }">&nbsp;</div>
            <!-- <img src="/assets/Moon.png" alt="Moon Planet" /> -->
        </div>
        
        <div class="planet-container__right">
            <TabMenu :menu="['Lune', 'Mars', 'Europe', 'Titan']" @planet-selected="handlePlanetSelected" />

            <PlanetInfo :currentPlanetIndex="currentPlanet" :planets="planets" />
        </div>
    </div>
</template>

<style scoped>  
    .planet-container {
        display: flex;
        justify-content: space-between;
        align-items: center;
        padding: var(--spacing-800) var(--spacing-200);
    }
    .planet-container__left {
        position: relative;
        width: 50%;
        height: 480px;
    }

    .planet-container__left .planet-img {
        position: absolute;
        top: 0;
        left: 0;
        width: 481px;
        height: 480px;
        opacity: 0;
        background-size: cover;
        transition: all 0.3s ease-in-out;
    }
    .planet-img.active {
        opacity: 1;
    }
    .moon {
        background: url("../../assets/Moon.png") no-repeat center center;
    }
    .mars {
        background: url("../../assets/Mars.png") no-repeat center center;
        z-index: 10;
    }
    .europa {
        background: url("../../assets/Europa.png") no-repeat center center;
    }
    .titan {
        background: url("../../assets/Titan.png") no-repeat center center;
    }

    .planet-container__right {
        width: 50%;
    }

    @media screen and (max-width: 1100px) {
        .planet-container {
            flex-direction: column;
            justify-content: center;
            align-items: center;
            gap: var(--spacing-400);
            padding: var(--spacing-100) var(--spacing-200);
        }
        .planet-container__left {
            height: 300px;
        }
        .planet-container__left .planet-img {
            width: 300px;
            height: 300px;
        }

        .planet-container__right {
            width: 75%;
            text-align: center;
        }
        ul.tab-menu {
            justify-content: center;
        }
    }

    @media screen and (max-width: 768px) {
        .planet-container__left {
            height: 150px;
        }
        .planet-container__left .planet-img {
            width: 150px;
            height: 150px;
        }
        .planet-container__right {
            width: 100%;
        }
    }
</style>