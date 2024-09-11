<template>
  <div class="container">
    <h2>Mobile Unit Location</h2>
    <div id="map" class="map-container"></div>

    <!-- Navigation Links -->
    <nuxt-link to="/mobile-units/check-in" class="link">Back to Check-in</nuxt-link>
  </div>
</template>

<script>
export default {
  data() {
    return {
      locations: [{
          id: 1,
          name: "Mobile Unit 1",
          latitude: 40.7128,
          longitude: -74.0060,
          status: "Active", // e.g., Active or Inactive
        },
        {
          id: 2,
          name: "Mobile Unit 2",
          latitude: 34.0522,
          longitude: -118.2437,
          status: "Inactive",
        },]
    }
  },
  async mounted() {
    try {
      const res = await this.$axios.get('/api/mobile-units/location');
      this.locations = res.data;
      this.initMap();
    } catch (error) {
      console.error(error);
    }
  },
  methods: {
    initMap() {
      const map = new google.maps.Map(document.getElementById('map'), {
        zoom: 10,
        center: { lat: 0, lng: 0 } // Default center
      });

      this.locations.forEach(location => {
        const marker = new google.maps.Marker({
          position: { lat: location.lat, lng: location.lng },
          map: map,
          title: `Mobile Unit at ${location.address}`
        });
      });
    }
  }
}
</script>

<style scoped>
.container {
  max-width: 800px;
  margin: 0 auto;
  padding: 20px;
  text-align: center;
}

.map-container {
  width: 100%;
  height: 400px;
  margin-bottom: 20px;
  background-color: #f0f0f0;
  border: 1px solid #ccc;
  border-radius: 5px;
  display: flex;
  justify-content: center;
  align-items: center;
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