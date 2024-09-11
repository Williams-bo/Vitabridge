<template>
  <div class="manage-appointments-container">
    <h2>Manage Appointments</h2>
    <ul class="appointments-list">
      <li v-for="appointment in appointments" :key="appointment.id" class="appointment-item">
        <div class="appointment-details">
          <strong>{{ appointment.patientName }}</strong> - {{ appointment.date }} - {{ appointment.reason }}
          <select v-model="appointment.status" @change="updateStatus(appointment)" class="status-select">
            <option value="pending">Pending</option>
            <option value="completed">Completed</option>
            <option value="canceled">Canceled</option>
          </select>
        </div>
      </li>
    </ul>
    <div class="back-link">
      <nuxt-link to="/telemedicine/dashboard-doctor">Back to Dashboard</nuxt-link>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      appointments: [{ id: 1, patientName: 'John Doe', date: '2024-09-10', reason: 'Check-up', status: 'pending' },
      { id: 2, patientName: 'Jane Smith', date: '2024-09-12', reason: 'Consultation', status: 'completed' },]
    }
  },
  async mounted() {
    const doctorId = 1; // Example doctor ID
    try {
      const res = await this.$axios.get(`/api/appointments/doctor/${doctorId}`);
      this.appointments = res.data;
    } catch (error) {
      console.error(error);
    }
  },
  methods: {
    async updateStatus(appointment) {
      try {
        await this.$axios.put(`/api/appointments/${appointment.id}/update`, {
          status: appointment.status
        });
        alert('Appointment status updated');
      } catch (error) {
        console.error(error);
        alert('Failed to update status');
      }
    }
  }
}
</script>
     
<style scoped>
.manage-appointments-container {
  background: #fff;
  border-radius: 8px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
  padding: 20px;
  max-width: 600px;
  margin: 50px auto;
}

h2 {
  color: #0056b3;
  margin-bottom: 20px;
}

.appointments-list {
  list-style: none;
  padding: 0;
}

.appointment-item {
  background: #f9f9f9;
  border-radius: 4px;
  padding: 15px;
  margin-bottom: 10px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.appointment-details {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.status-select {
  padding: 5px;
  border: 1px solid #ddd;
  border-radius: 4px;
}

.back-link {
  margin-top: 20px;
}

.back-link nuxt-link {
  color: #0056b3;
  text-decoration: none;
  font-weight: bold;
}

.back-link nuxt-link:hover {
  text-decoration: underline;
}
</style>
