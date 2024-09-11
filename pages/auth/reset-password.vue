<template>
  <div class="reset-password-container">
    <h2>Reset Password</h2>
    <div class="form-group">
      <input type="password" v-model="newPassword" placeholder="New Password" class="input-field" />
    </div>
    <div class="form-group">
      <input type="password" v-model="confirmPassword" placeholder="Confirm Password" class="input-field" />
    </div>
    <button class="button" @click="resetPassword">Reset Password</button>
  </div>
</template>


<script>
export default {
  data() {
    return {
      newPassword: '',
      confirmPassword: ''
    }
  },
  methods: {
    async resetPassword() {
      if (this.newPassword !== this.confirmPassword) {
        alert('Passwords do not match');
        return;
      }
      try {
        const token = this.$route.query.token; // Assume token is passed in URL
        await this.$axios.post('/api/auth/reset-password', {
          password: this.newPassword,
          token
        });
        alert('Password reset successful');
        this.$router.push('/login');
      } catch (error) {
        console.error(error);
        alert('Failed to reset password');
      }
    }
  }
}
</script>

<style scoped>
.reset-password-container {
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
</style>
