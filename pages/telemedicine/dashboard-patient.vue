<template>
  <div class="patient-dashboard-container">
    <h2>Patient Dashboard</h2>
    
    <div class="appointments-section">
      <h3>Upcoming Appointments</h3>
      <ul class="appointments-list">
        <li v-for="appointment in appointments" :key="appointment.id" class="appointment-item">
          {{ appointment.date }} - {{ appointment.reason }}
        </li>
      </ul>
    </div>
    
    <div class="records-section">
      <h3>Health Records</h3>
      <ul class="records-list">
        <li v-for="record in records" :key="record.id" class="record-item">
          {{ record.date }} - {{ record.diagnosis }}
        </li>
      </ul>
    </div>

    <div class="actions-link">
      <nuxt-link to="/telemedicine/appointment-booking" class="action-link">Book Appointment</nuxt-link>
      <nuxt-link to="/telemedicine/appointment-feedback" class="action-link">Submit Feedback</nuxt-link>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      appointments: [{ id: 1, date: '2024-09-15', reason: 'Routine Check-up' },
        { id: 2, date: '2024-09-20', reason: 'Follow-up Consultation' }],
      records: [{ id: 1, date: '2024-08-25', diagnosis: 'Flu' },
        { id: 2, date: '2024-08-30', diagnosis: 'Allergy' }]
    }
  },
  async mounted() {
    const patientId = 1; // Example patientId
    try {
      const resAppointments = await this.$axios.get(`/api/appointments/patient/${patientId}`);
      this.appointments = resAppointments.data;
      
      const resRecords = await this.$axios.get(`/api/records/${patientId}`);
      this.records = resRecords.data;
    } catch (error) {
      console.error(error);
    }
  }
}
</script>

<style scoped>
.patient-dashboard-container {
  background: #f4f6f8;
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

.appointments-section, .records-section {
  margin-bottom: 30px;
}

h3 {
  color: #0056b3;
  margin-bottom: 10px;
}

.appointments-list, .records-list {
  list-style: none;
  padding: 0;
}

.appointment-item, .record-item {
  background: #ffffff;
  border-radius: 4px;
  padding: 10px;
  margin-bottom: 10px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.actions-link {
  margin-top: 20px;
}

.action-link {
  display: inline-block;
  color: #007bff;
  text-decoration: none;
  font-weight: bold;
  margin-right: 15px;
}

.action-link:hover {
  text-decoration: underline;
}
</style>
