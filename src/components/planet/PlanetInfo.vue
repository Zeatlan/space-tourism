<script setup lang='ts'>
import { computed } from "vue";
const props = defineProps({
    currentPlanetIndex: Number,
    planets: Array<Object>,
});

const getName = computed(() => props.planets[props.currentPlanetIndex]?.name);
const getDescription = computed(() => props.planets[props.currentPlanetIndex]?.description);
const getDistance = computed(() => props.planets[props.currentPlanetIndex]?.distance);
const getTime = computed(() => props.planets[props.currentPlanetIndex]?.time);
</script>

<template>
    <div>
        <h2 class="text-preset-2">{{ getName }}</h2>
        <p class="text-preset-9">
            {{ getDescription }}
        </p>

        <div class="line"></div>

        <div class="planet-container__right-stats">
            <div class="planet-container__right-stats-item">
                <p class="text-preset-7">Distance Moy.</p>
                <h3 class="text-preset-6">{{ getDistance}}</h3>
            </div>

            <div class="planet-container__right-stats-item">
                <p class="text-preset-7">Est. temps de trajet</p>
                <h3 class="text-preset-6">{{ getTime }}</h3>
            </div>
        </div>
    </div>
</template>

<style scoped>
    h2 {
        text-transform: uppercase;
        margin: var(--spacing-300) 0 var(--spacing-100) 0;
    }
    p {
        color: var(--blue-300);
    }
    .line {
        width: 100%;
        height: 1px;
        background: var(--white);
        margin: var(--spacing-300) 0;
        opacity: 0.25;
    }

    .planet-container__right-stats {
        display: flex;
        justify-content: space-between;
        align-items: center;
    }
    .planet-container__right-stats-item h3,
    .planet-container__right-stats-item p {
        margin: 0;
    }
    .planet-container__right-stats-item p {
        margin-bottom: var(--spacing-50);
    }
    @media screen and (max-width: 1100px) {
        .line {
            display: block;
            margin: var(--spacing-200) 0;
        }
        .planet-container__right-stats-item h3 {
            font-size: 32px;
        }
    }
</style>