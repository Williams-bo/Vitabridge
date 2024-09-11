<template>
  <div class="video-call-container">
    <h2>Telemedicine Video Call</h2>
    
    <div v-if="callInProgress">
      <!-- This could be an iframe for an external video call service like Twilio, or custom WebRTC -->
      <iframe
        v-if="videoCallUrl"
        :src="videoCallUrl"
        class="video-frame"
        frameborder="0"
        allow="camera; microphone; fullscreen; encrypted-media"
      ></iframe>
      <button class="button" @click="endCall">End Call</button>
    </div>
    <div v-else>
      <button class="button" @click="startCall">Start Video Call</button>
    </div>
    
    <nuxt-link to="/telemedicine/dashboard-patient" class="back-link">Back to Dashboard</nuxt-link>
  </div>
</template>


<script>
export default {
  data() {
    return {
      callInProgress: false,
      videoCallUrl: null
    }
  },
  methods: {
    async startCall() {
      try {
        const res = await this.$axios.post('/api/video-call/initiate', {
          doctorId: 1, // Example doctor ID
          patientId: 2 // Example patient ID
        });
        this.videoCallUrl = res.data.url;
        this.callInProgress = true;
      } catch (error) {
        console.error(error);
        alert('Failed to initiate video call');
      }
    },
    async endCall() {
      try {
        await this.$axios.post('/api/video-call/end', {
          doctorId: 1, // Example doctor ID
          patientId: 2 // Example patient ID
        });
        this.callInProgress = false;
        this.videoCallUrl = null;
        alert('Call ended');
      } catch (error) {
        console.error(error);
        alert('Failed to end call');
      }
    }
  }
}
</script>

<style scoped>
.video-call-container {
  background: #f4f6f8;
  border-radius: 8px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
  padding: 20px;
  max-width: 800px;
  margin: 50px auto;
  text-align: center;
}

h2 {
  color: #007bff;
  margin-bottom: 20px;
}

.video-frame {
  width: 100%;
  height: 500px; /* Adjust height as needed */
  border-radius: 8px;
  margin-bottom: 20px;
}

.button {
  background-color: #007bff;
  color: #ffffff;
  border: none;
  padding: 10px 20px;
  border-radius: 4px;
  cursor: pointer;
  font-size: 16px;
  margin: 10px;
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
