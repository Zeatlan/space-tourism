<script setup lang='ts'>
import CrewPagination from './CrewPagination.vue';
import { ref } from 'vue';

const selectedCrew = ref(0);

const crews = [
    {
        title: "Commander",
        name: "Douglas Hurley",
        description: "Douglas Gerald Hurley is an American engineer, former Marine Corps pilot and former NASA astronaut. He launched into space for the third time as commander of Crew Dragon Demo-2.",
        image: "douglas-hurley.png"
    },
    {
        title: "Mission Specialist",
        name: "Mark Shuttleworth",
        description: "Mark Richard Shuttleworth is the founder and CEO of Canonical, the company behind the Linux-based Ubuntu operating system. Shuttleworth became the first South African to travel to space as a space tourist.",
        image: "mark-shuttleworth.png"
    },
    {
        title: "Pilot",
        name: "Victor Glover",
        description: "Pilot on the first operational flight of the SpaceX Crew Dragon to the International Space Station. Glover is a commander in the U.S. Navy where he pilots an F/A-18.He was a crew member of Expedition 64, and served as a station systems flight engineer. ",
        image: "victor-glover.png"
    },
    {
        title: "Flight Engineer",
        name: "Anousheh Ansari",
        description: "Anousheh Ansari is an Iranian American engineer and co-founder of Prodea Systems. Ansari was the fourth self-funded space tourist, the first self-funded woman to fly to the ISS, and the first Iranian in space. ",
        image: "anousheh-ansari.png"
    }
]

const handleCrewSelected = (index: number) => {
    selectedCrew.value = index;
}
</script>

<template>
    <div class="crew-wrapper">
        <div class="crew-wrapper__left-pan">
            <div class="left-pan__introduction">
                <h3 class="text-preset-4">{{ crews[selectedCrew].title }}</h3>
                <h2 class="text-preset-3">{{ crews[selectedCrew].name }}</h2>
                <p class="text-preset-9">{{ crews[selectedCrew].description }}</p>
            </div>

            <CrewPagination :crews="crews" @crew-selected="handleCrewSelected" />
        </div>

        <div class="crew-wrapper__right-pan">
            <div class="crew-image bg-image-1" :class="{ active: selectedCrew === 0 }"></div>
            <div class="crew-image bg-image-2" :class="{ active: selectedCrew === 1 }"></div>
            <div class="crew-image bg-image-3" :class="{ active: selectedCrew === 2 }"></div>
            <div class="crew-image bg-image-4" :class="{ active: selectedCrew === 3 }"></div>
        </div>
    </div>
</template> 

<style scoped>
.crew-wrapper {
    display: flex;
    align-items: center;
    justify-content: space-between;
    height: 70vh;
}
.crew-wrapper__left-pan {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    width: 40%;
    height: inherit;
}

.left-pan__introduction {
    padding: var(--spacing-1000) 0 0 0;
}
.left-pan__introduction h2,
.left-pan__introduction h3 {
    text-transform: uppercase;
    margin: 0;
}
.left-pan__introduction h3 {
    opacity: 0.5;
}
.left-pan__introduction h2 {
    margin: var(--spacing-200) 0 var(--spacing-100) 0;
}
.left-pan__introduction p {
    color: var(--blue-300);
}

.crew-wrapper__right-pan {
    position: relative;
    width: 40%;
    height: inherit;
}
.crew-image {
    position: absolute;
    bottom: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-size:contain;
    background-repeat: no-repeat;
    opacity: 0;
    transition: all 0.3s ease-in-out;
}

.crew-image.active {
    opacity: 1;
}

.crew-image.bg-image-1 {
    background-image: url("../../assets/crews/douglas-hurley.png");
    z-index: 0;
}
.crew-image.bg-image-2 {
    background-image: url("../../assets/crews/mark-shuttleworth.png");
    z-index: 5;
}
.crew-image.bg-image-3 {
    background-image: url("../../assets/crews/victor-glover.png");
    z-index: 10;
}
.crew-image.bg-image-4 {
    background-image: url("../../assets/crews/anousheh-ansari.png");
    z-index: 15;
}
</style>