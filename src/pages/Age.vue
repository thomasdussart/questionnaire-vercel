<template>
  <v-responsive>
    <div class="categories">
      <div class="centered-row">
        <h4 class="questions"></h4>
        <v-card
          v-for="(age, index) in ageArray"
          :color="getColor(index)"
          :key="age"
          class="card d-flex justify-center align-center text-white"
          @click="handleNext(age)"
        >
          {{ age }}
        </v-card>
      </div>
    </div>
  </v-responsive>
</template>

<script setup>
import { randomColor } from "@/components/RandomColor.vue";

if (!localStorage.getItem("token")) {
  window.location.href = "/";
}

const ageArray = [
  "-12 ans",
  "12 ans",
  "13 ans",
  "14 ans",
  "15 ans",
  "16 ans",
  "17 ans",
  "18 ans",
  "+18 ans",
];

const handleNext = (age) => {
  const parsedAge = age.replace(/ans/g, "");
  console.log(parsedAge);
  localStorage.setItem("age", parsedAge);
  window.location.href = "/ecole";
};

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
  justify-content: space-around;
  align-items: center;
  flex-wrap: wrap;
  gap: 20px;
  padding: 20px;
}

.card {
  width: 200px;
  height: 200px;
  border-radius: 20px;
  text-align: center;
}
</style>
