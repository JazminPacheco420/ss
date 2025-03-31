<template>
  <form class="form" @submit.prevent="register">
    <label class="form-label" for="email">Email:</label>
    <input v-model="email" class="form-input" type="email" id="email" placeholder="Email" />
    <p v-if="errorEmail" class="error">{{ errorEmail }}</p>

    <label class="form-label" for="password">Password:</label>
    <input v-model="password" class="form-input" type="password" id="password" placeholder="Password" />
    <p v-if="errorPassword" class="error">{{ errorPassword }}</p>

    <label class="form-label" for="passwordRepeat">Repite la contraseña:</label>
    <input v-model="passwordRepeat" class="form-input" type="password" id="passwordRepeat" placeholder="Repite la contraseña" />
    <p v-if="errorPasswordRepeat" class="error">{{ errorPasswordRepeat }}</p>

    <p v-if="error" class="error">{{ error }}</p>

    <input class="form-submit" type="submit" value="Sign Up" />
  </form>
</template>

<script>
export default {
  data() {
    return {
      email: "",
      password: "",
      passwordRepeat: "",
      error: "",
      errorEmail: "",
      errorPassword: "",
      errorPasswordRepeat: "",
    };
  },
  methods: {
    register() {
      this.errorEmail = "";
      this.errorPassword = "";
      this.errorPasswordRepeat = "";
      this.error = "";

      if (!this.validateEmail(this.email)) {
        this.errorEmail = "Introduce un email válido.";
      }
      if (this.password.length < 6) {
        this.errorPassword = "La contraseña debe tener al menos 6 caracteres.";
      }
      if (this.password !== this.passwordRepeat) {
        this.errorPasswordRepeat = "Las contraseñas no coinciden.";
      }

      if (!this.errorEmail && !this.errorPassword && !this.errorPasswordRepeat) {
        console.log("Registro correcto:", this.email, this.password);
        // Aquí iría la llamada a la API
      } else {
        this.error = "Revisa los campos.";
      }
    },
    validateEmail(email) {
      return /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(email);
    },
  },
};
</script>

<style scoped>
.error {
  color: #ff4a96;
  font-size: 0.9rem;
  margin-top: 5px;
}
</style>
