<template>
  <div class="doctor-dashboard-container">
    <h2>Doctor Dashboard</h2>
    
    <div class="appointments-section">
      <h3>Upcoming Appointments</h3>
      <ul class="appointments-list">
        <li v-for="appointment in appointments" :key="appointment.id" class="appointment-item">
          {{ appointment.date }} - {{ appointment.patientName }} - {{ appointment.reason }}
        </li>
      </ul>
    </div>
    
    <div class="records-section">
      <h3>Patient Records</h3>
      <ul class="records-list">
        <li v-for="record in records" :key="record.id" class="record-item">
          {{ record.patientName }} - {{ record.diagnosis }}
        </li>
      </ul>
    </div>

    <div class="manage-link">
      <nuxt-link to="/telemedicine/appointment-management">Manage Appointments</nuxt-link>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      appointments: [{ id: 1, date: '2024-09-10', patientName: 'John Doe', reason: 'Check-up' },
        { id: 2, date: '2024-09-12', patientName: 'Jane Smith', reason: 'Consultation' }],
      records: [{ id: 1, patientName: 'John Doe', diagnosis: 'Flu' },
        { id: 2, patientName: 'Jane Smith', diagnosis: 'Allergy' }]
    }
  },
  async mounted() {
    const doctorId = 1; // Example doctorId
    try {
      const resAppointments = await this.$axios.get(`/api/appointments/doctor/${doctorId}`);
      this.appointments = resAppointments.data;

      const resRecords = await this.$axios.get(`/api/records/${doctorId}`);
      this.records = resRecords.data;
    } catch (error) {
      console.error(error);
    }
  }
}
</script>

<style scoped>
.doctor-dashboard-container {
  background: #f8f9fa;
  border-radius: 8px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
  padding: 20px;
  max-width: 800px;
  margin: 50px auto;
}

h2 {
  color: #0056b3;
  margin-bottom: 20px;
}

.appointments-section, .records-section {
  margin-bottom: 30px;
}

h3 {
  color: #004085;
  margin-bottom: 10px;
}

.appointments-list, .records-list {
  list-style: none;
  padding: 0;
}

.appointment-item, .record-item {
  background: #fff;
  border-radius: 4px;
  padding: 10px;
  margin-bottom: 10px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.manage-link {
  margin-top: 20px;
}

.manage-link nuxt-link {
  color: #0056b3;
  text-decoration: none;
  font-weight: bold;
}

.manage-link nuxt-link:hover {
  text-decoration: underline;
}
</style>