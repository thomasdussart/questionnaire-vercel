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

// const colors = [
//   "#93C5FD", // Bleu pastel
//   "#A5B4FC", // Indigo doux
//   "#C4B5FD", // Lavande doux
//   "#D8B4FE", // Mauve pastel
//   "#F0ABFC", // Rose doux];
// ];

const colors = [
  "#3B82F6", // Bleu intense (point de départ stable)
  "#4C8EF7", // Bleu doux intermédiaire
  "#5EA5FA", // Bleu ciel équilibré
  "#6FBDFB", // Bleu très clair, lumineux
  "#5ACFEA", // Cyan doux intermédiaire
  "#4BC3D2", // Cyan-turquoise doux, moins saturé
  "#3EB8C4", // Turquoise doux équilibré
  "#32AFC2", // Bleu-turquoise légèrement plus profond (point d'arrivée stable)
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
