<template>
  <v-responsive>
    <div class="container">
      <div class="questions">
        <div
          class="question"
          v-for="(question, index) in questions"
          :key="question"
        >
          <v-card
            class="card d-flex justify-center align-center text-white text-fit"
            :color="randomColor()"
            dark
            @click="toggleSelection(index)"
          >
            <span v-if="isSelected(index)" class="selected-mark"></span>
            {{ question }}
          </v-card>
        </div>
      </div>
      <div class="next">
        <v-btn @click="handleNext()">Suivant</v-btn>
      </div>
    </div>
  </v-responsive>
</template>

<script setup>
import { ref } from "vue";
import { randomColor } from "../components/RandomColor.vue";
import axios from "axios";

// Tableau réactif pour stocker le texte des questions sélectionnées
const selectedAnswers = ref([]);

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

const toggleSelection = (index) => {
  const questionText = questions[index];
  const pos = selectedAnswers.value.indexOf(questionText);
  if (pos === -1) {
    selectedAnswers.value.push(questionText);
  } else {
    selectedAnswers.value.splice(pos, 1);
  }
};

const isSelected = (index) => {
  return selectedAnswers.value.includes(questions[index]);
};

let chosenCatString = localStorage.getItem("categories");
chosenCatString = chosenCatString
  .replace(["A - zÀ - ÿ"], "")
  .replace(/[\[\]"]/g, "");
let chosenCategories = chosenCatString.split(",");

const handleNext = async () => {
  const age = localStorage.getItem("age");
  const genre = localStorage.getItem("genre");
  const ecole = localStorage.getItem("ecole");
  const annee = localStorage.getItem("annee");

  await axios.post("http://localhost:1337/questions", {
    category: "Bien-être et santé",
    answers: selectedAnswers.value,
  });

  switch (chosenCategories[0]) {
    case "Vie relationnelle":
      chosenCategories = localStorage.getItem("categories");
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
    case "Ecrans":
      chosenCategories = JSON.parse(localStorage.getItem("categories"));
      chosenCategories.shift();
      localStorage.setItem("categories", JSON.stringify(chosenCategories));
      window.location.href = "/ecrans";
      break;
    default:
      await axios.post("http://localhost:1337/utilisateurs/create", {
        genre: genre,
        age: age,
        ecole: ecole,
        annee: annee,
      });
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
  font-size: 2rem;
}

.questions {
  display: flex;
  justify-content: center;
  gap: 10px;
  flex-wrap: wrap;
}

.card {
  width: fit-content;
  border-radius: 20px;
  padding: 30px;
  text-align: center;
  cursor: pointer;
}

/* Style pour le "V" indiquant la sélection */
.selected-mark:after {
  content: "\2714 \fe0e";
  color: #000;
  margin-right: 20px;
}
</style>
