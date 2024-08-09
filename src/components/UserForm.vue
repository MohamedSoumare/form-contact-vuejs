<template>
    <div>
      <h1>Formulaire de Saisie d'Informations</h1>
      <form @submit.prevent="handleSubmit">
        <div>
          <label for="name">Nom :</label>
          <input 
            id="name" 
            v-model="form.name" 
            type="text" 
            placeholder="Entrez votre nom"
          />
          <span v-if="errors.name" class="error">{{ errors.name }}</span>
        </div>
        
        <div>
          <label for="email">Email :</label>
          <input 
            id="email" 
            v-model="form.email" 
            type="email" 
            placeholder="Entrez votre email"
          />
          <span v-if="errors.email" class="error">{{ errors.email }}</span>
        </div>
        
        <div>
          <label for="phone" class="phone">Numéro de Téléphone :</label>
          <input 
            id="phone" 
            v-model="form.phone" 
            type="tel" 
            placeholder="Entrez votre numéro de téléphone"
          />
          <span v-if="errors.phone" class="error">{{ errors.phone }}</span>
        </div>
        
        <button type="submit">Soumettre</button>
        
        <p v-if="submitted" class="confirmation">Formulaire soumis avec succès !</p>
      </form>
    </div>
  </template>
  
<script>
  export default {
    name: 'UserForm',
    data() {
      return {
        form: {
          name: '',
          email: '',
          phone: ''
        },
        errors: {
          name: '',
          email: '',
          phone: ''
        },
        submitted: false
      };
    },
    methods: {
      validateForm() {
        this.errors = {
          name: '',
          email: '',
          phone: ''
        };
        
        let valid = true;
        
        if (!this.form.name) {
          this.errors.name = 'Le nom est requis.';
          valid = false;
        }
        
        if (!this.form.email) {
          this.errors.email = 'L\'email est requis.';
        } else if (!/\S+@\S+\.\S+/.test(this.form.email)) {
          this.errors.email = 'L\'email est invalide.';
          valid = false;
        }
        
        if (!this.form.phone) {
          this.errors.phone = 'Le numéro de téléphone est requis.';
        } else if (!/^\d{10}$/.test(this.form.phone)) {
          this.errors.phone = 'Le numéro de téléphone doit comporter 10 chiffres.';
          valid = false;
        }
        
        return valid;
      },
      handleSubmit() {
        if (this.validateForm()) {
          this.submitted = true;
         
        } else {
          this.submitted = false;
        }
      }
    }
  };

</script>
  
  <style scoped>

  .error {
    color: red;
    font-size: 0.9em;
  }
  
  .confirmation {
    color: green;
    font-size: 1.1em;
  }
  
  form {
    width: 600px;
    margin: 0 auto;
    padding: 1em;
    border: 1px solid #ccc;
    border-radius: 5px;
  }
  div {
    margin-bottom: 1em;
  }
  label {
    margin-bottom: 0.5em;
    color: #333333;
    display: block;
    margin-right:400px;
  }
  .phone{
        width: 220px; 
        margin-left: 30px;
  }
  input {
    border: 1px solid #CCCCCC;
    padding: 0.5em;
    font-size: 1em;
    width: 80%;
    box-sizing: border-box;
  }
  button {
    padding: 0.7em;
    color: white;
    background-color: #007BFF;
    border: none;
    border-radius: 5px;
    font-size: 1em;
    width: 40%;
    cursor: pointer;
  }
  button:hover {
    background-color: #0056b3;
  }
  
  </style>
  