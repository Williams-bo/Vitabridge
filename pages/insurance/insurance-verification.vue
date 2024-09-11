<template>
  <div class="container">
    <h2>Insurance Verification</h2>
    <div v-if="insuranceStatus">
      <h3>Status: {{ insuranceStatus.status }}</h3>
      <p>Coverage: {{ insuranceStatus.coverage }}</p>
    </div>
    <div v-else>
      <button class="button" @click="verifyInsurance">Verify Insurance</button>
    </div>
    <nuxt-link to="/insurance/payment" class="link">Proceed to Payment</nuxt-link>
  </div>
</template>

<script>
export default {
  data() {
    return {
      insuranceStatus: null
    }
  },
  methods: {
    async verifyInsurance() {
      try {
        const res = await this.$axios.post('/api/insurance/verify', {
          patientId: 1 // Example patient ID
        });
        this.insuranceStatus = res.data;
      } catch (error) {
        console.error(error);
        alert('Failed to verify insurance');
      }
    }
  }
}
</script>

<style scoped>
.container {
  max-width: 600px;
  margin: 0 auto;
  padding: 20px;
  text-align: center;
}

.button {
  padding: 8px 16px;
  background-color: #4CAF50;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

.button:hover {
  background-color: #45a049;
}

.link {
  display: block;
  margin-top: 20px;
  color: #007BFF;
  text-decoration: none;
}

.link:hover {
  text-decoration: underline;
}
</style>