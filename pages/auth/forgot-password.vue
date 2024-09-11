<template>
  <div class="forgot-password-container">
    <h2>Forgot Password</h2>
    <div class="form-group">
      <input type="email" v-model="email" placeholder="Enter your email" class="input-field" />
    </div>
    <button class="button" @click="requestPasswordReset">Submit</button>
    <p>Remember your password? <nuxt-link to="/auth/login">Login</nuxt-link></p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      email: ''
    }
  },
  methods: {
    async requestPasswordReset() {
      try {
        await this.$axios.post('/api/auth/forgot-password', { email: this.email });
        alert('Password reset link sent to your email');
      } catch (error) {
        console.error(error);
        alert('Failed to send reset link');
      }
    }
  }
}
</script>

<style scoped>
.forgot-password-container {
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

p {
  margin-top: 15px;
}
</style>
