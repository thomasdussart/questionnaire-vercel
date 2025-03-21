<template>
  <v-responsive>
    <div class="container">
      <h4 class="title"></h4>
      <div class="questions">
        <div
          class="question"
          v-for="(question, index) in questions"
          :key="question"
        >
          <v-card
            class="card d-flex justify-center align-center text-white text-fit"
            :color="getColor(index)"
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
import Swal from "sweetalert2";
import axios from "axios";

// Tableau réactif pour stocker le texte des questions sélectionnées
const selectedAnswers = ref([]);

const questions = [
  "Réseaux Sociaux",
  "Jeux vidéo",
  "Cyber harcèlement",
  "Sécurité en ligne",
  "Droit à l'image",
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

  await axios.post(
    "https://questionnaire-jeunesse-server.vercel.app/questions",
    {
      category: "Ecrans",
      answers: selectedAnswers.value,
    }
  );

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
    default:
      await axios.post(
        "https://questionnaire-jeunesse-server.vercel.app/utilisateurs/create",
        {
          genre: genre,
          age: age,
          ecole: ecole,
          annee: annee,
        }
      );
      Swal.fire({
        title: "Merci d'avoir répondu à toutes les questions!",
        icon: "success",
        confirmButtonText: "Fermer",
      }).then(() => {
        window.location.href = "/";
      });
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

.next {
  margin-top: 20px;
}

.v-btn {
  width: 10vw;
  padding: 25px;
  background-color: #3b82f6;
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
