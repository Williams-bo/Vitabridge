<template>
  <div class="record-container">
    <h2>Health Record Overview</h2>
    <ul class="record-list">
      <li v-for="record in records" :key="record.id" class="record-item">
        <p><strong>Date:</strong> {{ record.date }}</p>
        <p><strong>Diagnosis:</strong> {{ record.diagnosis }}</p>
        <p><strong>Prescriptions:</strong> {{ record.prescriptions.join(', ') }}</p>
      </li>
    </ul>
    
    <nuxt-link to="/health-records/update" class="update-link">Update Records</nuxt-link>
  </div>
</template>

<script>
export default {
  data() {
    return {
      records: [{ id: 1, date: '2024-09-01', diagnosis: 'Hypertension', prescriptions: ['Lisinopril', 'Amlodipine'] },
        { id: 2, date: '2024-06-15', diagnosis: 'Diabetes Type 2', prescriptions: ['Metformin', 'Insulin'] }]
    }
  },
  async mounted() {
    const patientId = 1; // Example patient ID
    try {
      const res = await this.$axios.get(`/api/records/${patientId}`);
      this.records = res.data;
    } catch (error) {
      console.error(error);
    }
  }
}
</script>

<style scoped>
.record-container {
  background: #ffffff;
  border-radius: 8px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
  padding: 20px;
  max-width: 800px;
  margin: 50px auto;
}

h2 {
  color: #007bff;
  margin-bottom: 20px;
}

.record-list {
  list-style-type: none;
  padding: 0;
}

.record-item {
  background: #f9f9f9;
  padding: 15px;
  margin-bottom: 20px;
  border-left: 4px solid #007bff;
  border-radius: 4px;
}

.record-item p {
  margin: 5px 0;
}

.update-link {
  display: inline-block;
  margin-top: 20px;
  color: #007bff;
  text-decoration: none;
  font-weight: bold;
}

.update-link:hover {
  text-decoration: underline;
}
</style>