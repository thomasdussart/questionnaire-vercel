<template>
  <v-responsive>
    <div class="categories">
      <div class="centered-row">
        <v-card
          :color="randomColor()"
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
import { randomColor } from "./RandomColor.vue";
import { onMounted } from "vue";

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
