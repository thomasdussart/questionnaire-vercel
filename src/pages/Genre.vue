<template>
  <v-responsive>
    <div class="categories">
      <div class="centered-row">
        <v-card
          :color="colors[3]"
          dark
          class="card d-flex justify-center align-center text-white"
          @click="handleNext(fille)"
        >
          {{ fille }}
        </v-card>
        <v-card
          :color="colors[5]"
          dark
          class="card d-flex justify-center align-center text-white"
          @click="handleNext(garcon)"
        >
          {{ garcon }}
        </v-card>

        <v-card
          :color="colors[7]"
          dark
          class="card d-flex justify-center align-center text-white"
          @click="handleNext(autre)"
        >
          {{ autre }}
        </v-card>
      </div>
    </div>
  </v-responsive>
</template>
<script setup>
let fille = "Fille";
let garcon = "Garçon";
let autre = "Autre";
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

// Fonction pour rediriger vers la catégorie choisie
const handleNext = (genre) => {
  // Envoi des réponses
  //   axios.post("http://localhost:3000/answers", {
  //     answers: [],
  //   });
  // Redirection vers la prochaine question
  localStorage.setItem("genre", genre);
  window.location.href = "/age";
};
</script>
<style>
.categories {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 80vh;
  padding: 10px;
  font-family: "Roboto", sans-serif;
  font-size: 3rem;
}

.centered-row {
  display: flex;
  justify-content: center;
  gap: 20px;
  margin-bottom: 20px;
  max-width: 80%;
}

.card {
  width: 400px;
  height: 200px;
  border-radius: 20px;
  padding: 30px;
  text-align: center;
}
</style>
