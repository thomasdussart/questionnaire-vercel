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
import { randomColor } from "../components/RandomColor.vue";

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

const colors = [
  "#FF5252", // rose
  "#448AFF", // bleu
  "#4CAF50", // vert
  "#ffc823", // jaune
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
  flex-wrap: wrap;
  gap: 20px;
  padding: 20px;
}

.card {
  width: 400px;
  height: 200px;
  border-radius: 20px;
  padding: 30px;
  text-align: center;
}
</style>
