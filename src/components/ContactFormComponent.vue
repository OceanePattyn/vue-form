<template>
    <div class="contact-form">
      <form @submit.prevent="submitForm">
        <!-- Nom -->
        <div class="mb-3">
          <label for="name" class="form-label">Nom</label>
          <input
            type="text"
            id="name"
            class="form-control"
            v-model="name"
            :class="{ 'is-invalid': nameError }"
          />
          <div class="invalid-feedback" v-if="nameError">{{ nameError }}</div>
        </div>
  
        <!-- Email -->
        <div class="mb-3">
          <label for="email" class="form-label">Email</label>
          <input
            type="email"
            id="email"
            class="form-control"
            v-model="email"
            :class="{ 'is-invalid': emailError }"
          />
          <div class="invalid-feedback" v-if="emailError">{{ emailError }}</div>
        </div>
  
        <!-- Sujet -->
        <div class="mb-3">
          <label for="subject" class="form-label">Sujet</label>
          <input
            type="text"
            id="subject"
            class="form-control"
            v-model="subject"
            :class="{ 'is-invalid': subjectError }"
          />
          <div class="invalid-feedback" v-if="subjectError">{{ subjectError }}</div>
        </div>
  
        <!-- Message -->
        <div class="mb-3">
          <label for="message" class="form-label">Message</label>
          <textarea
            id="message"
            class="form-control"
            rows="4"
            v-model="message"
            :class="{ 'is-invalid': messageError }"
          ></textarea>
          <div class="invalid-feedback" v-if="messageError">{{ messageError }}</div>
        </div>
  
        <!-- Bouton Envoyer -->
        <button type="submit" class="btn btn-primary">Envoyer</button>
      </form>
  
      <!-- Section des valeurs affichées après soumission -->
      <div v-if="submitted" class="mt-4">
        <h3>Résumé des informations envoyées :</h3>
        <p><strong>Nom :</strong> {{ name }}</p>
        <p><strong>Email :</strong> {{ email }}</p>
        <p><strong>Sujet :</strong> {{ subject }}</p>
        <p><strong>Message :</strong> {{ message }}</p>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        name: '',
        email: '',
        subject: '',
        message: '',
        nameError: null,
        emailError: null,
        subjectError: null,
        messageError: null,
        submitted: false
      };
    },
    methods: {
      validateForm() {
        this.nameError = !this.name ? "Le nom est requis" : null;
        this.emailError = !this.email ? "L'email est requis" : null;
        if (this.email && !/^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(this.email)) {
          this.emailError = "L'email n'est pas valide";
        }
        this.subjectError = !this.subject ? "Le sujet est requis" : null;
        this.messageError = !this.message ? "Le message est requis" : null;
  
        return !this.nameError && !this.emailError && !this.subjectError && !this.messageError;
      },
      submitForm() {
        if (this.validateForm()) {
          this.submitted = true;
        }
      }
    }
  };
  </script>
  
  <style scoped>
  .contact-form {
    max-width: 600px;
    margin: 0 auto;
  }
  
  .invalid-feedback {
    display: block;
  }
  </style>
  
  