<template>
  <div class="register-container">
    <h1>Register</h1>
    <form @submit.prevent="register">
      <div class="form-group">
        <label for="name">Name:</label>
        <input type="text" id="name" v-model="name" />
      </div>

      <div class="form-group">
        <label for="email">Email:</label>
        <input type="email" id="email" v-model="email" />
      </div>

      <div class="form-group">
        <label for="password">Password:</label>
        <input type="password" id="password" v-model="password" />
      </div>

      <div class="form-group">
        <label for="role">Role:</label>
        <select id="role" v-model="role">
          <option value="patient">Patient</option>
          <option value="doctor">Doctor</option>
          <option value="healthcare worker">Healthcare Worker</option>
        </select>
      </div>

      <button type="submit">Register</button>
    </form>
    <p>Already have an account? <nuxt-link to="/auth/login">Login</nuxt-link></p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      name: '',
      email: '',
      password: '',
      role: 'patient'
    };
  },
  methods: {
    async register() {
      // Call the backend API to register user
      const response = await fetch('/api/auth/register', {
        method: 'POST',
        body: JSON.stringify({
          name: this.name,
          email: this.email,
          password: this.password,
          role: this.role
        }),
        headers: { 'Content-Type': 'application/json' }
      });
      const data = await response.json();
      if (data.success) {
        this.$router.push('/login');
      }
    }
  }
};
</script>

<style scoped>
.register-container {
  background: #fff;
  border-radius: 8px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
  padding: 20px;
  max-width: 400px;
  margin: 50px auto;
}

h1 {
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

input, select {
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

p {
  text-align: center;
}
</style>
