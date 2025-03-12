<template>
  <v-responsive>
    <!-- Affichage de la question actuelle -->

    <div class="container">
      <!-- Boucle sur les options -->
      <div class="questions">
        <div class="question" v-for="question in questions" :key="question">
          <v-card
            class="card d-flex justify-center align-center text-white text-fit"
            :color="randomColor()"
            dark
          >
            {{ question }}
          </v-card>
        </div>
      </div>
      <div class="next">
        <v-btn @click="handleNext">Suivant</v-btn>
      </div>
    </div>
  </v-responsive>
</template>
<script setup>
import { randomColor } from "../components/RandomColor.vue";

let chosenCatString = localStorage.getItem("categories");
chosenCatString = chosenCatString
  .replace(["A - zÀ - ÿ"], "")
  .replace(/[\[\]"]/g, "");
let chosenCategories = chosenCatString.split(",");
const questions = [
  "Alimentation",
  "Sommeil",
  "Activité physique",
  "Hygiène corporelle",
  "Santé physique",
  "Stress et anxiété",
  "Dépression",
  "Estime de soi",
  "Réussite scolaire",
];

const handleNext = () => {
  // Envoi des réponses
  //   axios.post("http://localhost:3000/answers", {
  //     answers: [],
  //   });
  // Redirection vers la prochaine question
  switch (chosenCategories[0]) {
    case "Vie relationnelle":
      chosenCategories = JSON.parse(localStorage.getItem("categories"));
      chosenCategories.shift();
      localStorage.setItem("categories", JSON.stringify(chosenCategories));
      window.location.href = "/vie";
      break;
    case "Consommation et dépendance":
      chosenCategories = JSON.parse(localStorage.getItem("categories"));
      chosenCategories.shift();
      localStorage.setItem("categories", JSON.stringify(chosenCategories));
      window.location.href = "/consommation";
      break;
    case "Bien-être et santé":
      chosenCategories = JSON.parse(localStorage.getItem("categories"));
      chosenCategories.shift();
      localStorage.setItem("categories", JSON.stringify(chosenCategories));
      window.location.href = "/sante";
      break;
    case "Ecrans":
      chosenCategories = JSON.parse(localStorage.getItem("categories"));
      chosenCategories.shift();
      localStorage.setItem("categories", JSON.stringify(chosenCategories));
      window.location.href = "/ecrans";
      break;
    default:
      window.location.href = "/";
      break;
  }
};
</script>
<style scoped>
.container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 100vh;
  padding: 10px;
  font-family: "Roboto", sans-serif;
  font-size: 3rem;
}

.questions {
  display: flex;
  justify-content: center;
  gap: 20px;
  flex-wrap: wrap;
}

.card {
  width: 30vw;
  height: 200px;
  border-radius: 20px;
  padding: 30px;
  text-align: center;
}
</style>
