<template>
  <div class="update-container">
    <h2>Update Health Record</h2>
    
    <input type="text" v-model="diagnosis" placeholder="Diagnosis" class="input-field" />
    <input type="text" v-model="prescriptions" placeholder="Prescriptions (comma-separated)" class="input-field" />
    
    <button class="button" @click="updateRecord">Update Record</button>
    
    <nuxt-link to="/health-records/overview" class="back-link">Back to Overview</nuxt-link>
  </div>
</template>


<script>
export default {
  data() {
    return {
      diagnosis: '',
      prescriptions: ''
    }
  },
  methods: {
    async updateRecord() {
      const recordId = 1; // Example record ID
      try {
        await this.$axios.put(`/api/records/${recordId}/update`, {
          diagnosis: this.diagnosis,
          prescriptions: this.prescriptions.split(',').map(p => p.trim())
        });
        alert('Health record updated');
      } catch (error) {
        console.error(error);
        alert('Failed to update record');
      }
    }
  }
}
</script>

<style scoped>
.update-container {
  background: #ffffff;
  border-radius: 8px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
  padding: 20px;
  max-width: 600px;
  margin: 50px auto;
}

h2 {
  color: #007bff;
  margin-bottom: 20px;
}

.input-field {
  width: 100%;
  padding: 10px;
  margin-bottom: 20px;
  border: 1px solid #ccc;
  border-radius: 4px;
}

.button {
  background-color: #007bff;
  color: white;
  padding: 10px 20px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.button:hover {
  background-color: #0056b3;
}

.back-link {
  display: inline-block;
  margin-top: 20px;
  color: #007bff;
  text-decoration: none;
  font-weight: bold;
}

.back-link:hover {
  text-decoration: underline;
}
</style>