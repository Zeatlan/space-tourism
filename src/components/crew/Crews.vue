<script setup lang='ts'>
import CrewPagination from './CrewPagination.vue';
import { ref } from 'vue';

const selectedCrew = ref(0);

const crews = [
    {
        title: "Commandant",
        name: "Douglas Hurley",
        description: "Douglas Gerald Hurley est un ingénieur américain, ancien pilote du corps des Marines et ancien astronaute de la NASA. Il s'est envolé dans l'espace pour la troisième fois en tant que commandant de Crew Dragon Demo-2.",
        image: "douglas-hurley.png"
    },
    {
        title: "Spécialiste des missions",
        name: "Mark Shuttleworth",
        description: "Mark Richard Shuttleworth est le fondateur et le PDG de Canonical, la société à l'origine du système d'exploitation Ubuntu basé sur Linux. Shuttleworth est devenu le premier Sud-Africain à se rendre dans l'espace en tant que touriste spatial.",
        image: "mark-shuttleworth.png"
    },
    {
        title: "Pilote",
        name: "Victor Glover",
        description: "Pilote du premier vol opérationnel de la capsule SpaceX Crew Dragon vers la Station spatiale internationale. Glover est commandant dans la marine américaine où il pilote un F/A-18. Il a été membre de l'équipage de l'Expédition 64, et a servi en tant qu'ingénieur de vol des systèmes de la station. ",
        image: "victor-glover.png"
    },
    {
        title: "Mécanicienne de bord",
        name: "Anousheh Ansari",
        description: "Anousheh Ansari est une ingénieure irano-américaine, cofondatrice de Prodea Systems. Ansari a été la quatrième touriste spatial autofinancé, la première femme autofinancée à se rendre à l'ISS et la première Iranienne dans l'espace.", 
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

@media screen and (max-width: 1100px) {
    .crew-wrapper {
        flex-direction: column;
        height: 75vh;
    }
    .crew-wrapper__left-pan {
        width: 80%;
        justify-content: start;
        gap: var(--spacing-300);
    }
    .left-pan__introduction {
        padding: var(--spacing-200) 0 0 0;
        text-align: center;
    }
    .crew-pagination {
        justify-content: center;
    }
    .crew-wrapper__right-pan {
        width: 80%;
    }
    .crew-image {
        background-position: center;
    }
}

@media screen and (max-width: 768px) {
    .crew-pagination {
        margin-bottom: var(--spacing-200);
    }
}
</style>