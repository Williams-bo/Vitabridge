<template>
  <div class="education-container">
    <h2>Health Education</h2>
    
    <div v-for="content in educationContent" :key="content.id" class="content-item">
      <h3>{{ content.title }}</h3>
      <p>{{ content.description }}</p>
      <div v-if="content.type === 'video'" class="video-container">
        <video controls :src="content.url" class="video"></video>
      </div>
      <div v-else-if="content.type === 'article'" class="article-container">
        <a :href="content.url" target="_blank" class="read-more-link">Read More</a>
      </div>
    </div>
    
    <nuxt-link to="/health-education/feedback" class="feedback-link">Submit Feedback</nuxt-link>
  </div>
</template>

<script>
export default {
  data() {
    return {
      educationContent: [{ id: 1, title: 'Healthy Eating', description: 'Learn about healthy eating habits.', type: 'article', url: 'https://example.com/healthy-eating' },
        { id: 2, title: 'Exercise Tips', description: 'Tips for effective exercise routines.', type: 'video', url: 'https://example.com/exercise-tips.mp4' }]
    }
  },
  async mounted() {
    try {
      const res = await this.$axios.get('/api/health-education');
      this.educationContent = res.data;
    } catch (error) {
      console.error(error);
    }
  }
}
</script>

<style scoped>
.education-container {
  background: #ffffff;
  border-radius: 8px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
  padding: 20px;
  max-width: 800px;
  margin: 50px auto;
}

h2 {
  color: #007bff;
  margin-bottom: 20px;
}

.content-item {
  margin-bottom: 30px;
}

.content-item h3 {
  color: #333;
  margin: 10px 0;
}

.content-item p {
  color: #666;
}

.video-container {
  margin-top: 10px;
}

.video {
  width: 100%;
  max-width: 600px;
  border-radius: 4px;
}

.article-container {
  margin-top: 10px;
}

.read-more-link {
  color: #007bff;
  text-decoration: none;
  font-weight: bold;
}

.read-more-link:hover {
  text-decoration: underline;
}

.feedback-link {
  display: inline-block;
  margin-top: 20px;
  color: #007bff;
  text-decoration: none;
  font-weight: bold;
}

.feedback-link:hover {
  text-decoration: underline;
}
</style>