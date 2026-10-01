<template>
  <div class="app-shell">
    <AppHeader :active-view="activeView" @change-view="activeView = $event" />

    <main class="site-main">
      <HomeView v-if="activeView === 'home'" @change-view="activeView = $event" />
      <CarsView v-else-if="activeView === 'cars'" @change-view="activeView = $event" />

      <template v-else>
        <ContactView />

        <ContactForm
          form-title="Book a Test Drive"
          default-name=""
          @submit-form="handleFormSubmission"
        />

        <section v-if="customerAcknowledgement" class="ack-card" aria-live="polite">
          <h3>Customer Acknowledgement</h3>
          <p><strong>Thank you, {{ customerAcknowledgement.name }}.</strong></p>
          <p>Your test-drive request has been received.</p>
          <ul>
            <li><strong>Email:</strong> {{ customerAcknowledgement.email }}</li>
            <li><strong>Phone:</strong> {{ customerAcknowledgement.phone }}</li>
            <li><strong>Vehicle:</strong> {{ customerAcknowledgement.vehicle }}</li>
            <li><strong>Budget:</strong> ${{ Number(customerAcknowledgement.budget).toLocaleString() }}</li>
            <li><strong>Preferred contact:</strong> {{ customerAcknowledgement.preferredContact }}</li>
          </ul>
        </section>
      </template>
    </main>

    <AppFooter @change-view="activeView = $event" />
  </div>
</template>

<script setup>
import { ref } from 'vue'
import AppHeader from './components/AppHeader.vue'
import AppFooter from './components/AppFooter.vue'
import HomeView from './components/HomeView.vue'
import CarsView from './components/CarsView.vue'
import ContactView from './components/ContactView.vue'
import ContactForm from './components/ContactForm.vue'

const activeView = ref('home')
const customerAcknowledgement = ref(null)

function handleFormSubmission(formData) {
  customerAcknowledgement.value = formData
}
</script>
