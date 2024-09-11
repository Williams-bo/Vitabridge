<!-- layouts/default.vue -->
<template>
  <div>
    <header>
      <nav>
        <ul>
          <li><nuxt-link to="/">Home</nuxt-link></li>
          <li><nuxt-link to="/telemedicine/dashboard-patient">Patient Dashboard</nuxt-link></li>
          <li><nuxt-link to="/telemedicine/dashboard-doctor">Doctor Dashboard</nuxt-link></li>
          <li><nuxt-link to="/health-records/health-record-overview">Health Records</nuxt-link></li>
          <li><nuxt-link to="/insurance/insurance-selection">Insurance</nuxt-link></li>
          <li><nuxt-link to="/mobile-units/mobile-unit-checkin">Mobile Unit Check-in</nuxt-link></li>
          <li><nuxt-link to="/health-education/health-education">Health Education</nuxt-link></li>
        </ul>
      </nav>
    </header>
    <main>
      <nuxt />
    </main>
    <footer>
      <p>Footer Content Here</p>
    </footer>
  </div>
</template>

<style>
/* Add your CSS styles here */
header {
  background: #f5f5f5;
  padding: 1rem;
}
nav ul {
  list-style: none;
  display: flex;
  gap: 1rem;
}
nav a {
  text-decoration: none;
  color: #333;
}
</style>
