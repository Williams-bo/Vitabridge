<template>
  <div class="book-appointment-container">
    <h2>Book an Appointment</h2>
    <div class="form-group">
      <input type="date" v-model="date" class="input-field" />
    </div>
    <div class="form-group">
      <input type="time" v-model="time" class="input-field" />
    </div>
    <div class="form-group">
      <input type="text" v-model="reason" placeholder="Reason for Visit" class="input-field" />
    </div>
    <button class="button" @click="bookAppointment">Book Appointment</button>
    <div class="back-link">
      <nuxt-link to="/telemedicine/dashboard-patient">Back to Dashboard</nuxt-link>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      date: '',
      time: '',
      reason: ''
    }
  },
  methods: {
    async bookAppointment() {
      const patientId = 1; // Example patient ID
      try {
        await this.$axios.post('/api/appointments/create', {
          patientId,
          date: `${this.date} ${this.time}`,
          reason: this.reason
        });
        alert('Appointment booked successfully');
      } catch (error) {
        console.error(error);
        alert('Failed to book appointment');
      }
    }
  }
}
</script>

<style scoped>
.book-appointment-container {
  background: #fff;
  border-radius: 8px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
  padding: 20px;
  max-width: 400px;
  margin: 50px auto;
  text-align: center;
}

h2 {
  color: #0056b3;
  margin-bottom: 20px;
}

.form-group {
  margin-bottom: 15px;
}

.input-field {
  width: 100%;
  padding: 10px;
  border: 1px solid #ddd;
  border-radius: 4px;
}

.button {
  width: 100%;
  padding: 10px;
  background-color: #0056b3;
  color: #fff;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.button:hover {
  background-color: #004494;
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