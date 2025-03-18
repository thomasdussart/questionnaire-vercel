<template>
  <v-responsive>
    <div class="categories">
      <div class="centered-row">
        <v-card
          v-for="(ecole, index) in ecoleArray"
          :color="getColor(index)"
          :key="ecole"
          class="card d-flex justify-center flex-wrap align-center text-white"
          @click="handleNext(ecole)"
        >
          {{ ecole }}
        </v-card>
      </div>
    </div>
  </v-responsive>
</template>
<script setup>
import { randomColor } from "../components/RandomColor.vue";
// Fonction pour rediriger vers la catégorie choisie

const ecoleArray = [
  "ARH",
  "Lycée",
  "Collège",
  "Les Orchidées",
  "SAS Aux Sources",
  "Je ne fréquente pas d'école",
  "Autre",
];

const colors = [
  "#FF5252", // rose
  "#448AFF", // bleu
  "#4CAF50", // vert
  "#ffc823", // jaune
];

const getColor = (index) => {
  return colors[index % colors.length];
};

const handleNext = (ecole) => {
  localStorage.setItem("ecole", ecole);
  window.location.href = "/annee";
};
</script>
<style>
.categories {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 100vh;
  padding: 10px;
  font-family: "Roboto", sans-serif;
  font-size: 3rem;
}

.centered-row {
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
  gap: 20px;
  margin-bottom: 20px;
}

.card {
  width: 350px;
  height: 200px;
  border-radius: 20px;
  text-align: center;
}
</style>
