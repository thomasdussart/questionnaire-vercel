<template>
  <v-container class="fill-height d-flex justify-center align-center">
    <v-card class="pa-5" max-width="400">
      <v-card-title class="justify-center">
        <h3>Accès sécurisé</h3>
      </v-card-title>

      <v-card-text>
        <!-- hCaptcha Widget -->
        <div id="hcaptcha-container"></div>

        <v-btn
          class="mt-4"
          :disabled="!captchaValidated"
          color="primary"
          block
          @click="enterApp"
        >
          Entrer
        </v-btn>
      </v-card-text>
    </v-card>
  </v-container>
</template>

<script>
export default {
  data() {
    return {
      captchaValidated: false,
    };
  },
  mounted() {
    // Charger le script hCaptcha
    const script = document.createElement("script");
    script.src =
      "https://js.hcaptcha.com/1/api.js?onload=hcaptchaOnLoadCallback&render=explicit";
    script.async = true;
    script.defer = true;
    document.head.appendChild(script);

    // Callback global pour hCaptcha
    window.hcaptchaOnLoadCallback = () => {
      window.hcaptcha.render("hcaptcha-container", {
        sitekey: "ea480786-2294-4d9e-a9cc-8472ce720756", // 🔁 Remplace par ta vraie clé site
        callback: this.onCaptchaSuccess,
      });
    };
  },
  methods: {
    onCaptchaSuccess(token) {
      this.captchaValidated = true;
      localStorage("token", token);
      console.log("hCaptcha token:", token);
    },
    enterApp() {
      this.$router.push("/"); // Par exemple
    },
  },
};
</script>
