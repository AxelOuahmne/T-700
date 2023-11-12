<template>
  <div>
    <h2 class="mt-3">Modifier l'utilisateur {{ this.user.name }}</h2>

    <!-- Formulaire pour la modification de l'utilisateur -->
    <form @submit.prevent="updateUser" class="w-50 mx-auto mt-5" >
      <!-- Ajoutez des champs pour les informations de l'utilisateur -->
      <div>
        <label for="name"  class="form-label">Nom:</label>
        <input v-model="user.name" type="text" id="name"  class="form-control"  required>
      </div>

      <div>
        <label for="surname"  class="form-label">Prénom:</label>
        <input v-model="user.surname" type="text" id="surname" class="form-control"  required>
      </div>

      <div>
        <label for="email"  class="form-label">Email:</label>
        <input v-model="user.email" type="email" id="email" class="form-control"  required>
      </div>

      <!-- Ajoutez d'autres champs selon les informations que vous souhaitez modifier -->

      <!-- Bouton de soumission du formulaire -->
      <button type="submit" class="mt-4">Enregistrer les modifications</button>
    </form>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "EditUser",
  data() {
    return {
      userId: null, // L'ID de l'utilisateur que vous obtiendrez des paramètres d'URL
      user: {
        name: "",
        surname: "",
        email: "",
        // Ajoutez d'autres propriétés selon les informations que vous souhaitez modifier
      },
    };
  },

  mounted() {
    // Récupérez l'ID de l'utilisateur à partir des paramètres d'URL
    this.userId = this.$route.params.userId;

    // Chargez les informations de l'utilisateur à modifier
    this.getUserDetails();
  },

  methods: {
    async getUserDetails() {
      try {
        // Effectuez une requête GET pour obtenir les informations de l'utilisateur
        const response = await axios.get(`http://localhost:4000/api/users/${this.userId}`);

        // Remplissez les propriétés de l'utilisateur avec les informations récupérées
        this.user = response.data;
      } catch (error) {
        console.error("Erreur lors de la récupération des détails de l'utilisateur :", error);
      }
    },
    async updateUser() {
  try {
    console.log("Request Payload:", this.user);

    // Effectuez une requête PUT pour mettre à jour les informations de l'utilisateur
    await axios.put(`http://localhost:4000/api/users/${this.userId}`, { user: this.user });

    // Redirigez l'utilisateur vers la page des utilisateurs après la mise à jour
    this.$router.push({ name: 'allUsers' });
  } catch (error) {
    console.error("Erreur lors de la mise à jour de l'utilisateur :", error);
    console.log("Réponse du serveur :", error.response.data);
  }
}

  },
};
</script>

<style>
/* Ajoutez des styles CSS selon vos besoins */
</style>
