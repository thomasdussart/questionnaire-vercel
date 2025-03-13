<template>
  <v-responsive>
    <div class="categories">
      <div class="centered-row">
        <v-card
          v-for="category in categories"
          :key="category"
          :color="randomColor()"
          dark
          class="card d-flex justify-center align-center text-white"
          @click="toggleCategory(category)"
        >
          <!-- Conteneur qui sera flouté -->
          <div
            class="card-background"
            :class="{ 'blur-background': isSelected(category) }"
          >
            <span>{{ category }}</span>
          </div>
          <!-- Overlay du numéro qui n'est pas flouté -->
          <div v-if="isSelected(category)" class="number-overlay">
            {{ getCategoryNumber(category) }}
          </div>
        </v-card>
      </div>
      <div class="nextBtn">
        <v-btn @click="handleNext">Suivant</v-btn>
      </div>
    </div>
  </v-responsive>
</template>

<script setup>
import { ref } from "vue";
import { randomColor } from "../components/RandomColor.vue";
import Swal from "sweetalert2";
import axios from "axios";

let chosenCategories = [];
// Définition des catégories
const categories = [
  "Vie relationnelle",
  "Consommation et dépendance",
  "Bien-être et santé",
  "Ecrans",
];

// Variable réactive pour les catégories sélectionnées
const selectedCategories = ref([]);

// Toggle de la sélection d'une catégorie
const toggleCategory = (category) => {
  if (selectedCategories.value.includes(category)) {
    selectedCategories.value = selectedCategories.value.filter(
      (c) => c !== category
    );
  } else {
    selectedCategories.value.push(category);
  }
};

// Vérifie si une catégorie est sélectionnée
const isSelected = (category) => {
  localStorage.setItem("categories", JSON.stringify(selectedCategories.value));
  return selectedCategories.value.includes(category);
};

// Retourne le numéro d'ordre de la catégorie sélectionnée
const getCategoryNumber = (category) => {
  return selectedCategories.value.indexOf(category) + 1;
};

const handleNext = async () => {
  if (selectedCategories.value.length < 4) {
    Swal.fire({
      icon: "error",
      title: "Oops...",
      text: "Veuillez sélectionner l'ensemble des catégories",
    });
    return;
  }

  await axios.post("http://localhost:1337/new-categories", {
    categories: selectedCategories.value,
  });

  switch (selectedCategories.value[0]) {
    case "Vie relationnelle":
      console.log("Vie relationnelle");
      chosenCategories = JSON.parse(localStorage.getItem("categories"));
      chosenCategories.shift();
      localStorage.setItem("categories", JSON.stringify(chosenCategories));
      window.location.href = "/vie";
      break;
    case "Consommation et dépendance":
      console.log("Consommation et dépendance");
      chosenCategories = JSON.parse(localStorage.getItem("categories"));
      chosenCategories.shift();
      localStorage.setItem("categories", JSON.stringify(chosenCategories));
      window.location.href = "/consommation";
      break;
    case "Bien-être et santé":
      console.log("Bien-être et santé");
      chosenCategories = JSON.parse(localStorage.getItem("categories"));
      chosenCategories.shift();
      localStorage.setItem("categories", JSON.stringify(chosenCategories));
      window.location.href = "/sante";
      break;
    case "Ecrans":
      console.log("Ecrans");
      chosenCategories = JSON.parse(localStorage.getItem("categories"));
      chosenCategories.shift();
      localStorage.setItem("categories", JSON.stringify(chosenCategories));
      window.location.href = "/ecrans";
      break;
  }
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
  flex-wrap: wrap;
  justify-content: space-between;
  gap: 20px;
  margin-bottom: 20px;
}

.card {
  position: relative;
  cursor: pointer;
  width: 400px;
  height: 200px;
  border-radius: 20px;
  padding: 30px;
  text-align: center;
  overflow: hidden;
}

/* Conteneur qui sera flouté lorsqu'une catégorie est sélectionnée */
.card-background {
  position: relative;
  width: 100%;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
}

.blur-background {
  filter: blur(3px);
  transition: filter 0.3s;
}

/* Overlay pour le numéro, non flouté */
.number-overlay {
  position: absolute;
  top: 10px;
  right: 10px;
  background: rgba(0, 0, 0, 0.5);
  border-radius: 50%;
  width: 50px;
  height: 50px;
  display: flex;
  align-items: center;
  justify-content: center;
  color: white;
  font-weight: bold;
  z-index: 10;
}
</style>
