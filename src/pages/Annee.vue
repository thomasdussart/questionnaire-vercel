<template>
  <v-responsive>
    <div class="categories">
      <div class="centered-row">
        <v-card
          :color="randomColor()"
          v-for="annee in anneeArray"
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
  width: 400px;
  height: 200px;
  border-radius: 20px;
  padding: 30px;
  text-align: center;
}
</style>
