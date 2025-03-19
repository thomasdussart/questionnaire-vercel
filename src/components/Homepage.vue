<template>
  <v-responsive>
    <div class="categories">
      <div class="centered-row">
        <v-card
          :color="colors[0]"
          dark
          class="card d-flex justify-center align-center text-white"
          @click="handleStart()"
        >
          Commencer
        </v-card>
      </div>
    </div>
  </v-responsive>
</template>
<script setup>
import { onMounted } from "vue";

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

onMounted(() => {
  localStorage.removeItem("categories");
  localStorage.removeItem("genre");
  localStorage.removeItem("age");
  localStorage.removeItem("ecole");
  localStorage.removeItem("annee");
});
// Fonction pour rediriger vers la catégorie choisie
const handleStart = () => {
  window.location.href = "/genre";
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
