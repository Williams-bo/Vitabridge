<template>
  <div class="feedback-container">
    <h2>Appointment Feedback</h2>
    <div class="form-group">
      <textarea v-model="feedback" placeholder="Enter your feedback" class="input-field"></textarea>
    </div>
    <button class="button" @click="submitFeedback">Submit Feedback</button>
    <div class="back-link">
      <nuxt-link to="/telemedicine/dashboard-patient">Back to Dashboard</nuxt-link>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      feedback: ''
    }
  },
  methods: {
    async submitFeedback() {
      const appointmentId = 1; // Example appointment ID
      try {
        await this.$axios.post('/api/appointments/feedback', {
          appointmentId,
          feedback: this.feedback
        });
        alert('Feedback submitted');
      } catch (error) {
        console.error(error);
        alert('Failed to submit feedback');
      }
    }
  }
}
</script>

<style scoped>
.feedback-container {
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
  min-height: 100px; /* Ensure textarea has a reasonable height */
  resize: vertical; /* Allow vertical resizing */
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