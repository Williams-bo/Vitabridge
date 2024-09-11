<template>
  <div class="container">
    <h2>Select an Insurance Plan</h2>
    <ul class="insurance-list">
      <li v-for="plan in insurancePlans" :key="plan.id" class="insurance-item">
        <strong>{{ plan.name }}</strong> - {{ plan.details }}
        <button class="button" @click="selectPlan(plan.id)">Select</button>
      </li>
    </ul>
    <nuxt-link to="/insurance/verification" class="link">Verify Insurance</nuxt-link>
  </div>
</template>

<script>
export default {
  data() {
    return {
      insurancePlans: [{ id: 1, name: "Basic Plan", details: "Covers essential treatments and medications" },
        { id: 2, name: "Premium Plan", details: "Includes full coverage for surgeries and specialist care" },
        { id: 3, name: "Family Plan", details: "Coverage for family members, including preventive care" },]
    }
  },
  async mounted() {
    try {
      const res = await this.$axios.get('/api/insurance/plans');
      this.insurancePlans = res.data;
    } catch (error) {
      console.error(error);
    }
  },
  methods: {
    async selectPlan(planId) {
      try {
        await this.$axios.post('/api/insurance/link', {
          patientId: 1, // Example patient ID
          planId: planId
        });
        alert('Insurance plan linked');
      } catch (error) {
        console.error(error);
        alert('Failed to link insurance plan');
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

.insurance-list {
  list-style-type: none;
  padding: 0;
}

.insurance-item {
  margin-bottom: 20px;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 8px;
}

.button {
  margin-top: 10px;
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