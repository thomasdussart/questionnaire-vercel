<template>
  <v-responsive>
    <div class="categories">
      <div class="centered-row">
        <v-card
          color="#448AFF"
          dark
          class="card d-flex justify-center align-center text-white"
          @click="handleNext(fille)"
        >
          {{ fille }}
        </v-card>
        <v-card
          color="#4CAF50"
          dark
          class="card d-flex justify-center align-center text-white"
          @click="handleNext(garcon)"
        >
          {{ garcon }}
        </v-card>

        <v-card
          color="#ffc823"
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
