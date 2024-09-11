<template>
  <div class="container">
    <h2>Mobile Unit Check-in</h2>
    <input type="text" v-model="patientName" placeholder="Patient Name" class="input-field" />
    <button class="button" @click="checkInPatient">Check In</button>

    <!-- Navigation Links -->
    <nuxt-link to="/mobile-units/record-update" class="link">Update Records</nuxt-link>
    <nuxt-link to="/mobile-units/location" class="link">View Location</nuxt-link>
  </div>
</template>

<script>
export default {
  data() {
    return {
      patientName: ''
    }
  },
  methods: {
    async checkInPatient() {
      try {
        await this.$axios.post('/api/mobile-units/check-in', {
          patientName: this.patientName
        });
        alert('Check-in successful');
      } catch (error) {
        console.error(error);
        alert('Failed to check in');
      }
    }
  }
}
</script>

<style scoped>
.container {
  max-width: 600px;
  margin: 0 auto;
  padding: 20px;
  text-align: center;
}

.input-field {
  width: 100%;
  padding: 10px;
  margin-bottom: 20px;
  border: 1px solid #ccc;
  border-radius: 5px;
}

.button {
  padding: 10px 20px;
  background-color: #4CAF50;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

.button:hover {
  background-color: #45a049;
}

.link {
  display: block;
  margin-top: 20px;
  color: #007BFF;
  text-decoration: none;
}

.link:hover {
  text-decoration: underline;
}
</style>