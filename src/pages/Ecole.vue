<template>
  <v-responsive>
    <div class="categories">
      <div class="centered-row">
        <v-card
          :color="randomColor()"
          v-for="ecole in ecoleArray"
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

const handleNext = (ecole) => {
  // Envoi des réponses
  //   axios.post("http://localhost:3000/answers", {
  //     answers: [],
  //   });
  // Redirection vers la prochaine question
  localStorage.setItem("ecole", ecole);
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
  justify-content: center;
  flex-wrap: wrap;
  gap: 20px;
  margin-bottom: 20px;
}

.card {
  width: 400px;
  height: 200px;
  border-radius: 20px;
  padding: 30px;
  text-align: center;
}
</style>
