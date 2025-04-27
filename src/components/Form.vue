<template>
  <div class="container">
    <div class="form-container">
      <div class="progress-bar">
        <div class="step-info">
          <span>Étape {{ currentStep }}/6</span>
          <div class="progress-container">
            <div class="progress" :style="{ width: progressPercentage + '%' }"></div>
          </div>
        </div>
      </div>
      
      <form @submit.prevent="submitForm" class="form">
        <h1>{{ currentStep }}. {{ getStepTitle(currentStep) }}</h1>

        <!-- Étape 1 - Formation -->
        <div v-if="currentStep === 1">
          <div class="input-container">
            <select v-model="formData.typeFormation" required>
              <option value="" disabled selected>Type de formation</option>
              <option v-for="type in formationTypes" :key="type" :value="type">{{ type }}</option>
            </select>
            <span class="required-asterisk">*</span>
          </div>

          <div class="input-container">
            <select v-model="formData.domaine" required>
              <option value="" disabled selected>Domaine de formation</option>
              <option v-for="domaine in domaines" :key="domaine" :value="domaine">{{ domaine }}</option>
            </select>
            <span class="required-asterisk">*</span>
          </div>

          <div class="input-container">
            <select v-model="formData.formation" required>
              <option value="" disabled selected>Nom de la formation</option>
              <option v-for="formation in formations" :key="formation" :value="formation">{{ formation }}</option>
            </select>
            <span class="required-asterisk">*</span>
          </div>

          <div class="input-container">
            <select v-model="formData.campus" required>
              <option value="" disabled selected>Campus</option>
              <option v-for="campus in campusList" :key="campus" :value="campus">{{ campus }}</option>
            </select>
            <span class="required-asterisk">*</span>
          </div>

          <div class="input-container">
            <label for="rentree">Date de rentrée souhaitée</label>
            <input type="date" id="rentree" v-model="formData.dateRentree" required>
            <span class="required-asterisk">*</span>
          </div>
        </div>

        <!-- Étape 2 - Identité & coordonnées -->
        <div v-if="currentStep === 2">
          <div class="input-group">
            <div class="input-container">
              <input type="text" v-model="formData.nom" required placeholder="Nom">
              <span class="required-asterisk">*</span>
            </div>
            <div class="input-container">
              <input type="text" v-model="formData.prenom" required placeholder="Prénom">
              <span class="required-asterisk">*</span>
            </div>
            <div class="input-container">
              <select v-model="formData.genre" required placeholder="Genre">
                <option value="" disabled selected>Genre</option>
                <option value="H">Homme</option>
                <option value="F">Femme</option>
                <option value="A">Autre</option>
              </select>
              <span class="required-asterisk">*</span>
            </div>
          </div>

          <div class="input-group">
            <div class="input-container">
              <label for="dateNaissance">Date de naissance</label>
              <input type="date" id="dateNaissance" v-model="formData.dateNaissance" required>
              <span class="required-asterisk">*</span>
            </div>
            <div class="input-container">
              <input type="text" v-model="formData.lieuNaissance" required placeholder="Lieu de naissance">
              <span class="required-asterisk">*</span>
            </div>
          </div>

          <div class="input-container">
            <input type="text" v-model="formData.nationalite" required placeholder="Nationalité">
            <span class="required-asterisk">*</span>
          </div>

          <div class="input-group">
            <div class="input-container">
              <input type="text" v-model="formData.numSecu" placeholder="N° de sécurité sociale">
            </div>
            <div class="input-container">
              <input type="text" v-model="formData.numEtudiant" placeholder="N° étudiant (si applicable)">
            </div>
          </div>

          <div class="input-group">
            <div class="input-container">
              <input type="email" v-model="formData.email" required placeholder="Email">
              <span class="required-asterisk">*</span>
            </div>
            <div class="input-container">
              <input type="tel" v-model="formData.telephone" required placeholder="Téléphone">
              <span class="required-asterisk">*</span>
            </div>
          </div>

          <div class="input-container">
            <input v-model="formData.adresse" required placeholder="Adresse postale complète"></input>
            <span class="required-asterisk">*</span>
          </div>

          <div class="input-container">
            <input type="text" v-model="formData.zoneGeo" placeholder="Zone géographique / temps de transport">
          </div>
        </div>

        <div v-if="currentStep === 3">
  <div class="input-container">
    <select v-model="formData.situationFamiliale" required>
      <option value="" disabled selected>Situation familiale</option>
      <option v-for="situation in situationsFamiliales" :key="situation" :value="situation">
        {{ situation }}
      </option>
    </select>
    <span class="required-asterisk">*</span>
  </div>

  <div class="input-group">
    <div class="input-container">
      <input type="text" v-model="formData.urgenceNom" required placeholder="Personne à prévenir - Nom">
      <span class="required-asterisk">*</span>
    </div>
    <div class="input-container">
      <input type="tel" v-model="formData.urgenceTel" required placeholder="Personne à prévenir - Téléphone">
      <span class="required-asterisk">*</span>
    </div>
  </div>

  <div v-if="isMineur" class="input-group">
    <div class="input-container">
      <input type="text" v-model="formData.responsableNom" required placeholder="Responsable légal - Nom">
      <span class="required-asterisk">*</span>
    </div>
    <div class="input-container">
      <input type="tel" v-model="formData.responsableTel" required placeholder="Responsable légal - Téléphone">
      <span class="required-asterisk">*</span>
    </div>
  </div>
</div>

<!-- Étape 4 - Parcours -->
<div v-if="currentStep === 4">
  <div class="input-group">
    <div class="input-container">
      <input type="text" v-model="formData.dernierDiplome" required placeholder="Dernier diplôme obtenu">
      <span class="required-asterisk">*</span>
    </div>
    <div class="input-container">
      <input type="text" v-model="formData.etablissement" required placeholder="Établissement">
      <span class="required-asterisk">*</span>
    </div>
  </div>

  <div class="input-group">
    <div class="input-container">
      <input type="number" v-model="formData.anneeObtention" required placeholder="Année d'obtention">
      <span class="required-asterisk">*</span>
    </div>
    <div class="input-container">
      <input type="text" v-model="formData.ville" required placeholder="Ville">
      <span class="required-asterisk">*</span>
    </div>
  </div>

  <div class="input-container file-upload">
    <label>Relevés ou bulletins</label>
    <input type="file" @change="handleFileUpload($event, 'bulletins')" multiple accept=".pdf,.jpg,.png">
    <span class="required-asterisk">*</span>
  </div>

  <div class="input-container">
    <select v-model="formData.statutActuel" required>
      <option value="" disabled selected>Statut actuel</option>
      <option v-for="statut in statuts" :key="statut" :value="statut">{{ statut }}</option>
    </select>
    <span class="required-asterisk">*</span>
  </div>

  <div class="input-container">
    <input type="text" v-model="formData.experiencePro" placeholder="Expériences professionnelles"></input>
  </div>

  <div class="input-container file-upload">
    <label>CV et lettre de motivation</label>
    <input type="file" @change="handleFileUpload($event, 'cv')" multiple accept=".pdf">
    <span class="required-asterisk">*</span>
  </div>
</div>

<!-- Étape 5 - Financement -->
<div v-if="currentStep === 5">
  <div class="input-container">
    <select v-model="formData.modeFinancement" required>
      <option value="" disabled selected>Mode de financement</option>
      <option v-for="mode in modesFinancement" :key="mode" :value="mode">{{ mode }}</option>
    </select>
    <span class="required-asterisk">*</span>
  </div>

  <div v-if="needsEmployerInfo" class="input-group">
    <div class="input-container">
      <input type="text" v-model="formData.employeurNom" required placeholder="Nom de l'employeur/organisme">
      <span class="required-asterisk">*</span>
    </div>
    <div class="input-container">
      <input type="text" v-model="formData.employeurContact" required placeholder="Contact">
      <span class="required-asterisk">*</span>
    </div>
  </div>

  <div class="input-container file-upload">
    <label>Pièces justificatives</label>
    <input type="file" @change="handleFileUpload($event, 'documents')" multiple accept=".pdf,.jpg,.png">
    <span class="required-asterisk">*</span>
  </div>
</div>

<!-- Étape 6 - Récapitulatif -->
<div v-if="currentStep === 6">
  <div class="recap-container">
    <h3 class="recap-title">Récapitulatif de votre inscription</h3>
    
    <div class="recap-grid">
      <!-- Formation -->
      <div class="recap-section">
        <h4>Formation</h4>
        <div class="recap-item">
          <div class="item-label">Type de formation :</div>
          <div class="item-value">{{ formData.typeFormation }}</div>
        </div>
        <div class="recap-item">
          <div class="item-label">Domaine :</div>
          <div class="item-value">{{ formData.domaine }}</div>
        </div>
        <div class="recap-item">
          <div class="item-label">Formation :</div>
          <div class="item-value">{{ formData.formation }}</div>
        </div>
        <div class="recap-item">
          <div class="item-label">Campus :</div>
          <div class="item-value">{{ formData.campus }}</div>
        </div>
        <div class="recap-item">
          <div class="item-label">Date de rentrée :</div>
          <div class="item-value">{{ formData.dateRentree }}</div>
        </div>
      </div>

      <!-- Identité -->
      <div class="recap-section">
        <h4>Identité & Coordonnées</h4>
        <div class="recap-item">
          <div class="item-label">Nom complet :</div>
          <div class="item-value">{{ formData.nom }} {{ formData.prenom }}</div>
        </div>
        <div class="recap-item">
          <div class="item-label">Genre :</div>
          <div class="item-value">{{ formData.genre }}</div>
        </div>
        <div class="recap-item">
          <div class="item-label">Date de naissance :</div>
          <div class="item-value">{{ formData.dateNaissance }}</div>
        </div>
        <div class="recap-item">
          <div class="item-label">Lieu de naissance :</div>
          <div class="item-value">{{ formData.lieuNaissance }}</div>
        </div>
        <div class="recap-item">
          <div class="item-label">Nationalité :</div>
          <div class="item-value">{{ formData.nationalite }}</div>
        </div>
        <div class="recap-item">
          <div class="item-label">N° Sécurité sociale :</div>
          <div class="item-value">{{ formData.numSecu || 'Non renseigné' }}</div>
        </div>
        <div class="recap-item">
          <div class="item-label">N° Étudiant :</div>
          <div class="item-value">{{ formData.numEtudiant || 'Non renseigné' }}</div>
        </div>
      </div>

      <!-- Contact -->
      <div class="recap-section">
        <h4>Contact</h4>
        <div class="recap-item">
          <div class="item-label">Email :</div>
          <div class="item-value">{{ formData.email }}</div>
        </div>
        <div class="recap-item">
          <div class="item-label">Téléphone :</div>
          <div class="item-value">{{ formData.telephone }}</div>
        </div>
        <div class="recap-item">
          <div class="item-label">Adresse :</div>
          <div class="item-value">{{ formData.adresse }}</div>
        </div>
        <div class="recap-item">
          <div class="item-label">Zone géographique :</div>
          <div class="item-value">{{ formData.zoneGeo || 'Non renseigné' }}</div>
        </div>
      </div>

      <!-- Situation -->
      <div class="recap-section">
        <h4>Situation personnelle</h4>
        <div class="recap-item">
          <div class="item-label">Situation familiale :</div>
          <div class="item-value">{{ formData.situationFamiliale }}</div>
        </div>
        <div class="recap-item">
          <div class="item-label">Contact d'urgence :</div>
          <div class="item-value">{{ formData.urgenceNom }} - {{ formData.urgenceTel }}</div>
        </div>
        <div v-if="isMineur" class="recap-item">
          <div class="item-label">Responsable légal :</div>
          <div class="item-value">{{ formData.responsableNom }} - {{ formData.responsableTel }}</div>
        </div>
      </div>

      <!-- Parcours -->
      <div class="recap-section">
        <h4>Parcours</h4>
        <div class="recap-item">
          <div class="item-label">Dernier diplôme :</div>
          <div class="item-value">{{ formData.dernierDiplome }}</div>
        </div>
        <div class="recap-item">
          <div class="item-label">Établissement :</div>
          <div class="item-value">{{ formData.etablissement }} - {{ formData.ville }}</div>
        </div>
        <div class="recap-item">
          <div class="item-label">Année d'obtention :</div>
          <div class="item-value">{{ formData.anneeObtention }}</div>
        </div>
        <div class="recap-item">
          <div class="item-label">Statut actuel :</div>
          <div class="item-value">{{ formData.statutActuel }}</div>
        </div>
        <div v-if="formData.experiencePro" class="recap-item">
          <div class="item-label">Expériences professionnelles :</div>
          <div class="item-value">{{ formData.experiencePro }}</div>
        </div>
      </div>

      <!-- Financement -->
      <div class="recap-section">
        <h4>Financement</h4>
        <div class="recap-item">
          <div class="item-label">Mode de financement :</div>
          <div class="item-value">{{ formData.modeFinancement }}</div>
        </div>
        <div v-if="needsEmployerInfo" class="recap-item">
          <div class="item-label">Employeur/Organisme :</div>
          <div class="item-value">{{ formData.employeurNom }}</div>
        </div>
        <div v-if="needsEmployerInfo" class="recap-item">
          <div class="item-label">Contact employeur :</div>
          <div class="item-value">{{ formData.employeurContact }}</div>
        </div>
      </div>
    </div>
  </div>

  <div class="validation-container">
    <div class="checkbox-group">
      <div class="checkbox-item">
        <input type="checkbox" id="attestation" v-model="formData.attestation" required>
        <label for="attestation">J'atteste de l'exactitude des informations fournies</label>
        <span class="required-asterisk">*</span>
      </div>

      <div class="checkbox-item">
        <input type="checkbox" id="rgpd" v-model="formData.rgpd" required>
        <label for="rgpd">J'accepte le traitement de mes données personnelles</label>
        <span class="required-asterisk">*</span>
      </div>
    </div>
  </div>
</div>

        <!-- Autres étapes... -->

        <div class="buttons">
          <button type="button" @click="prevStep" v-if="currentStep > 1" class="return">Retour</button>
          <button type="submit" v-if="currentStep < 6">Suivant</button>
          <button type="submit" v-if="currentStep === 6">Envoyer</button>
        </div>
      </form>
    </div>

    <div class="steps-container">
      <h2>Étapes :</h2>
      <div class="step" :class="{ active: currentStep === i + 1 }" v-for="(step, i) in 6" :key="i">
        {{ i + 1 }}. {{ getStepTitle(i + 1) }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      currentStep: 1,
      formData: {
        // Étape 1
        typeFormation: '',
        domaine: '',
        formation: '',
        campus: '',
        dateRentree: '',

        // Étape 2
        nom: '',
        prenom: '',
        genre: '',
        dateNaissance: '',
        lieuNaissance: '',
        nationalite: '',
        numSecu: '',
        numEtudiant: '',
        email: '',
        telephone: '',
        adresse: '',
        zoneGeo: '',

        // Étape 3
      situationFamiliale: '',
      urgenceNom: '',
      urgenceTel: '',
      responsableNom: '',
      responsableTel: '',

      // Étape 4
      dernierDiplome: '',
      etablissement: '',
      anneeObtention: '',
      ville: '',
      bulletins: [],
      statutActuel: '',
      experiencePro: '',
      cv: [],

      // Étape 5
      modeFinancement: '',
      employeurNom: '',
      employeurContact: '',
      documents: [],

      // Étape 6
      attestation: false,
      rgpd: false
      },
      // Données statiques pour les select
      formationTypes: ['Initial', 'Alternance', 'Continue'],
      domaines: ['Informatique', 'Marketing', 'Management', 'Communication'],
      formations: ['Bachelor Développeur Web', 'Master Data Science', 'MBA Marketing Digital'],
      campusList: ['Paris', 'Lyon', 'Marseille', 'Bordeaux'],
      situationsFamiliales: ['Célibataire', 'Marié(e)', 'Pacsé(e)', 'Divorcé(e)'],
    statuts: ['Étudiant', 'Salarié', 'Demandeur d\'emploi', 'Autre'],
    modesFinancement: ['Personnel', 'Entreprise', 'Organisme', 'Autre']
    }
  },

  computed: {
  progressPercentage() {
    return (this.currentStep / 6) * 100;
  },
  isMineur() {
    if (!this.formData.dateNaissance) return false;
    const age = new Date().getFullYear() - new Date(this.formData.dateNaissance).getFullYear();
    return age < 18;
  },
  needsEmployerInfo() {
    return ['Entreprise', 'Organisme'].includes(this.formData.modeFinancement);
  },
  formDataSummary() {
  const summary = {};
  for (const [key, value] of Object.entries(this.formData)) {
    if (value && typeof value !== 'object' && 
        key !== 'attestation' && key !== 'rgpd') {
      summary[key] = value;
    }
  }
  return summary;
}
},
  
methods: {
  prevStep() {
    if (this.currentStep > 1) {
      this.currentStep--;
    }
  },

  getStepTitle(step) {
    const titles = {
      1: 'Formation souhaitée',
      2: 'Identité & coordonnées',
      3: 'Situation personnelle',
      4: 'Parcours',
      5: 'Financement & PJ',
      6: 'Récapitulatif'
    };
    return titles[step] || '';
  },

  submitForm() {
    try {
      if (this.currentStep === 6) {
        // Envoyer les données
        console.log('Formulaire soumis:', this.formData);
        // Réinitialiser le formulaire
        this.resetForm();
      } else {
        this.currentStep++;
      }
    } catch (error) {
      console.error('Erreur lors de la soumission:', error);
    }
  },

  resetForm() {
    this.formData = {
      typeFormation: '',
      domaine: '',
      formation: '',
      campus: '',
      dateRentree: '',
      // ... réinitialiser les autres champs
    };
    this.currentStep = 1;
  },

  handleFileUpload(event, type) {
    if (event.target.files) {
      this.formData[type] = Array.from(event.target.files);
    }
  },

  formatLabel(key) {
    if (!key) return '';
    return key
      .replace(/([A-Z])/g, ' $1')
      .replace(/^./, str => str.toUpperCase());
  }
}
}

</script>


<style scoped>
body {
  font-family: Arial, sans-serif;
  background-color: #ffffff;

}
input, select{
  color: #0F0127;
  background-color: #ffffff;
  width: 90%;
  padding: 10px;
  margin: 5px 0;
  border: 2px solid #f6f0ff;
  border-radius: 5px;
  transition: border-color 0.3s ease;
}
select {
  width: 94%;
}
input::placeholder {
  color: #ccc;
}
input:focus {
  border-color: #7009fb;
  outline: none;
}
.form {
  width: 600px;
  display: flex;
  flex-direction: column;

  justify-content: center;
}
.input-container {
  position: relative;
}

.required-asterisk {
  font-size: 1.5rem;
  position: absolute;
  top: -8px;
  right: 12px;
  color: #7009fb;
  font-weight: bold;
}
.container {
  display: flex;
  align-items: flex-start;
}

.form-container {
  flex: 6;
  display: flex;
  flex-direction: column;
  align-items: center; 
  justify-content: space-between;
  padding: 20px;

}
/* Styles pour le récapitulatif */
.recap-container {
  width: 100%;
  max-width: 800px;
  margin: 0 auto;
  padding: 20px;
  background-color: #f8f9fa;
  border-radius: 10px;
}

.recap-title {
  text-align: center;
  color: #7009fb;
  margin-bottom: 30px;
}

.recap-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 20px;
}

.recap-section {
  background-color: white;
  padding: 20px;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0,0,0,0.1);
}

.recap-section h4 {
  color: #fcb33a;
  margin-bottom: 15px;
  padding-bottom: 10px;
  border-bottom: 2px solid #f6f0ff;
}

.recap-item {
  margin-bottom: 15px;
  display: flex;
  flex-direction: column;
}

.item-label {
  font-weight: 600;
  color: #0F0127;
  margin-bottom: 5px;
}

.item-value {
  color: #4a4a4a;
}

.validation-container {
  margin-top: 30px;
  width: 600px;
  background-color: white;
  padding: 20px;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0,0,0,0.1);
}

.checkbox-group {
  display: flex;
  flex-direction: column;
  gap: 15px;
}

.checkbox-item {
  display: flex;
  align-items: flex-start;
  gap: 10px;
  position: relative;
}

.checkbox-item input[type="checkbox"] {
  width: auto;
  margin-top: 4px;
}

.checkbox-item label {
  flex: 1;
  font-size: 14px;
  color: #4a4a4a;
}

.steps-container {
  display: flex;
  flex: 1;
  flex-direction: column;
  /* position: fixed;
  top: 0;
  right: 0; */
  width: 300px;
  height: 80vh;
  align-items: start;
  justify-content: center;
  text-align: start;
  background-color: #dcc2fe;
  margin-left: 50px;
  padding: 20px;
  border: 1px solid #ccc;
  border-radius: 5px;
}

.step {
  text-align: start;
  margin-bottom: 10px;
  padding: 5px 10px;
  border-radius: 25px;
  background-color: #fee1b4;
  transition: background-color 0.5s ease, color 0.3s ease;
}

.step.active {
  background-color: #fcb33a;
  color: white;
  font-weight: bold;
}

.buttons {
  margin-top: 20px;
  padding: 20px;
  display: flex;
  justify-content: space-between;
}

button {

  padding: 10px 20px;
  background-color: #fcb33a;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

button:hover {
  background-color: #7009fb;
}
.progress-bar {
  display: flex;
  justify-content: center;
  align-items: center;
  margin-bottom: 20px;
}

.step-info {
  display: flex;
  align-items: center;
}

.step-info span {
  font-weight: bold;
  margin-right: 10px;
}

.progress-container {
  width: 300px;
  height: 5px;
  background-color: #f6f0ff;
  border-radius: 10px;
  overflow: hidden;
}

.progress {
  height: 100%;
  background-color: #fcb33a;
  transition: width 0.5s ease-in-out;
}
.return {
background-color: transparent;
  color: #9e9e9e;
  padding: 10px 20px 10px 0;
  text-decoration: underline;
  transition: color 0.3s ease;
}
.return:hover {
background-color: transparent;
  color: #7009fb;
}


</style>