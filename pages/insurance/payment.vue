<template>
  <div class="container">
    <h2>Process Payment</h2>
    <div>
      <input v-model="amount" type="number" placeholder="Amount to pay" class="input-field" />
      <button class="button" @click="processPayment">Pay with Insurance</button>
    </div>
    <nuxt-link to="/insurance/selection" class="link">Back to Selection</nuxt-link>
  </div>
</template>

<script>
export default {
  data() {
    return {
      amount: 0
    }
  },
  methods: {
    async processPayment() {
      try {
        await this.$axios.post('/api/insurance/pay', {
          patientId: 1, // Example patient ID
          amount: this.amount
        });
        alert('Payment processed successfully');
      } catch (error) {
        console.error(error);
        alert('Failed to process payment');
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

.input-field {
  width: 100%;
  padding: 10px;
  margin-bottom: 20px;
  border: 1px solid #ccc;
  border-radius: 5px;
}

.button {
  padding: 10px 20px;
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