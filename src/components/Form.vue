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
      <h1>{{ currentStep }}. {{ getStepTitle(currentStep) }}</h1>
      <form @submit.prevent="submitForm">
        <div v-if="currentStep === 1">
          <div class="input-container">
    <select v-model="selected" class="dropdown" required>
      <option value="" disabled selected>Sélectionnez une option</option>
      <option v-for="option in options" 
              :key="option.value" 
              :value="option.value">
        {{ option.text }}
      </option>
    </select>
    <span class="required-asterisk">*</span>
  </div>
          <div class="input-container">
            <input type="text" id="name" v-model="name" required placeholder="Nom">
            <span class="required-asterisk">*</span>
          </div>
        </div>
        <div v-if="currentStep === 2" class="input-container">
          <input type="email" id="email" v-model="email" required placeholder="Email">
          <span class="required-asterisk">*</span>
        </div>
        <div v-if="currentStep === 3">
          <label for="phone">Téléphone :</label>
          <input type="tel" id="phone" v-model="phone" required>
        </div>
        <div v-if="currentStep === 4">
          <label for="address">Adresse :</label>
          <input id="address" v-model="address" required></input>
        </div>
        <div v-if="currentStep === 5">
          <label for="message">Message :</label>
          <input id="message" v-model="message" required></input>
        </div>
        <div v-if="currentStep === 6">
          <h2>Récapitulatif</h2>
          <p><strong>Nom :</strong> {{ name }}</p>
          <p><strong>Email :</strong> {{ email }}</p>
          <p><strong>Téléphone :</strong> {{ phone }}</p>
          <p><strong>Adresse :</strong> {{ address }}</p>
          <p><strong>Message :</strong> {{ message }}</p>
        </div>
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
      name: '',
      email: '',
      phone: '',
      address: '',
      message: ''
    }
  },
  computed: {
    progressPercentage() {
      return (this.currentStep / 6) * 100;
    }
  },
  methods: {
    prevStep() {
      this.currentStep--;
    },
    getStepTitle(step) {
      switch (step) {
        case 1:
          return 'Formation';
        case 2:
          return 'Coordonnées';
        case 3:
          return 'Situation perso.';
        case 4:
          return 'Parcours';
        case 5:
          return 'Financement & PJ';
        case 6:
          return 'Récapitulatif';
      }
    },
    submitForm() {
      if (this.currentStep === 6) {
        this.name = '';
        this.email = '';
        this.phone = '';
        this.address = '';
        this.message = '';
      } else {
        this.currentStep++;
      }
    }
  }
}

</script>


<style scoped>
body {
  font-family: Arial, sans-serif;
  background-color: #ffffff;

}
input {
  color: #0F0127;
  background-color: #ffffff;
  width: 90%;
  padding: 10px;
  margin: 5px 0;
  border: 2px solid #f6f0ff;
  border-radius: 5px;
  transition: border-color 0.3s ease;
}
input::placeholder {
  color: #ccc;
}
input:focus {
  border-color: #7009fb;
  outline: none;
}
.input-container {
  position: relative;
}

.required-asterisk {
  position: absolute;
  top: 8px;
  right: 20px;
  color: #7009fb;
  font-weight: bold;
}
.container {
  display: flex;
  justify-content: center;
  align-items: flex-start;
  margin-top: 50px;
}

.form-container {
  max-width: 500px;
  padding: 20px;

}

.steps-container {
  display: flex;
  flex-direction: column;
  position: fixed;
  top: 0;
  right: 0;
  width: 300px;
  height: 100vh;
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
  display: flex;
  justify-content: space-between;
}

button {
  margin-left: 10px;
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