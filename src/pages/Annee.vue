<template>
  <v-responsive>
    <div class="categories">
      <div class="centered-row">
        <v-card
          v-for="(annee, index) in anneeArray"
          :color="getColor(index)"
          :key="annee"
          class="card d-flex justify-center align-center text-white"
          @click="handleNext(annee)"
        >
          {{ annee }}
        </v-card>
      </div>
    </div>
  </v-responsive>
</template>

<script setup>
import { randomColor } from "../components/RandomColor.vue";

const anneeArray = [
  "1ère secondaire",
  "2ème secondaire",
  "3ème secondaire",
  "4ème secondaire",
  "5ème secondaire",
  "6ème secondaire",
  "7ème secondaire",
  "Différenciée",
];

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

const handleNext = (annee) => {
  const parsedAnnee = annee.replace(/secondaire/g, "");
  console.log(parsedAnnee);
  localStorage.setItem("annee", parsedAnnee);
  window.location.href = "/categories";
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
  justify-content: space-between;
  flex-wrap: wrap;
  gap: 20px;
  padding: 20px;
}

.card {
  width: 300px;
  height: 200px;
  border-radius: 20px;
  text-align: center;
}
</style>
