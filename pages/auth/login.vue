<template>
  <div class="login-container">
    <h2>Login</h2>
    <form @submit.prevent="login">
      <div class="form-group">
        <label for="email">Email:</label>
        <input type="email" id="email" v-model="email" required />
      </div>
      <div class="form-group">
        <label for="password">Password:</label>
        <input type="password" id="password" v-model="password" required />
      </div>
      <button type="submit">Login</button>
      <p>Don't have an account? <nuxt-link to="/auth/register">Register</nuxt-link></p>
      <nuxt-link to="/auth/forgot-password">Forgot Password?</nuxt-link>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      email: '',
      password: ''
    };
  },
  methods: {
    async login() {
      // Call the backend API to authenticate user
      const response = await fetch('/api/auth/login', {
        method: 'POST',
        body: JSON.stringify({ email: this.email, password: this.password }),
        headers: { 'Content-Type': 'application/json' }
      });
      const data = await response.json();
      if (data.token) {
        localStorage.setItem('token', data.token);
        this.$router.push('/dashboard');
      }
    }
  }
};
</script>

<style scoped>
.login-container {
  background: #fff;
  border-radius: 8px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
  padding: 20px;
  max-width: 400px;
  margin: 50px auto;
}

h2 {
  color: #0056b3;
  text-align: center;
}

.form-group {
  margin-bottom: 15px;
}

label {
  display: block;
  margin-bottom: 5px;
}

input {
  width: 100%;
  padding: 8px;
  border: 1px solid #ddd;
  border-radius: 4px;
}

button {
  width: 100%;
  padding: 10px;
  background-color: #0056b3;
  color: #fff;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

button:hover {
  background-color: #004494;
}
</style>
