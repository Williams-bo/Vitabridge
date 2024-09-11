<template>
  <div class="feedback-container">
    <h2>Submit Feedback</h2>
    
    <textarea v-model="feedback" placeholder="Enter your feedback" class="input-field"></textarea>
    <button class="button" @click="submitFeedback">Submit Feedback</button>
    
    <nuxt-link to="/health-education/health-education" class="back-link">Back to Content</nuxt-link>
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
      try {
        await this.$axios.post('/api/health-education/feedback', {
          feedback: this.feedback
        });
        alert('Feedback submitted');
        this.feedback = ''; // Clear the input after submitting
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
  background: #f4f6f8;
  border-radius: 8px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
  padding: 20px;
  max-width: 600px;
  margin: 50px auto;
  text-align: center;
}

h2 {
  color: #007bff;
  margin-bottom: 20px;
}

.input-field {
  width: 100%;
  height: 150px; /* Adjust height as needed */
  padding: 10px;
  border-radius: 4px;
  border: 1px solid #ddd;
  margin-bottom: 20px;
  font-size: 16px;
}

.button {
  background-color: #007bff;
  color: #ffffff;
  border: none;
  padding: 10px 20px;
  border-radius: 4px;
  cursor: pointer;
  font-size: 16px;
}

.button:hover {
  background-color: #0056b3;
}

.back-link {
  display: inline-block;
  color: #007bff;
  text-decoration: none;
  font-weight: bold;
  margin-top: 20px;
}

.back-link:hover {
  text-decoration: underline;
}
</style>