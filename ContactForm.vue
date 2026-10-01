<template>
  <section class="container form-section">
    <h2>{{ formTitle }}</h2>

    <form class="test-drive-form" novalidate @submit.prevent="submitForm">
      <div class="form-grid">
        <div class="field full-width">
          <label for="name">Full Name</label>
          <input id="name" v-model.trim="form.name" type="text" />
          <p v-if="errors.name" class="error-message">{{ errors.name }}</p>
        </div>

        <div class="field">
          <label for="email">Email</label>
          <input id="email" v-model.trim="form.email" type="email" />
          <p v-if="errors.email" class="error-message">{{ errors.email }}</p>
        </div>

        <div class="field">
          <label for="phone">Phone Number</label>
          <input id="phone" v-model.trim="form.phone" type="tel" />
          <p v-if="errors.phone" class="error-message">{{ errors.phone }}</p>
        </div>

        <div class="field">
          <label for="budget">Maximum Budget ($)</label>
          <input id="budget" v-model.number="form.budget" type="number" min="1000" step="500" />
          <p v-if="errors.budget" class="error-message">{{ errors.budget }}</p>
        </div>

        <div class="field">
          <label for="vehicle">Select Vehicle</label>
          <select id="vehicle" v-model="form.vehicle">
            <option disabled value="">Choose a vehicle</option>x
            <option v-for="vehicle in vehicleOptions" :key="vehicle" :value="vehicle">
              {{ vehicle }}
            </option>
          </select>
          <p v-if="errors.vehicle" class="error-message">{{ errors.vehicle }}</p>
        </div>

        <fieldset class="field full-width radio-group">
          <legend>Preferred Contact Method</legend>
          <label><input v-model="form.preferredContact" type="radio" value="Phone" /> Phone</label>
          <label><input v-model="form.preferredContact" type="radio" value="Email" /> Email</label>
          <p v-if="errors.preferredContact" class="error-message">{{ errors.preferredContact }}</p>
        </fieldset>

        <div class="field">
          <label for="date">Preferred Date</label>
          <input id="date" v-model="form.date" type="date" />
          <p v-if="errors.date" class="error-message">{{ errors.date }}</p>
        </div>

        <div class="field">
          <label for="time">Preferred Time</label>
          <input id="time" v-model="form.time" type="time" />
          <p v-if="errors.time" class="error-message">{{ errors.time }}</p>
        </div>

        <div class="field full-width">
          <label for="message">Additional Message</label>
          <textarea id="message" v-model.trim="form.message" rows="4"></textarea>
        </div>

        <div class="field full-width checkbox-field">
          <label>
            <input v-model="form.consent" type="checkbox" />
            I confirm that the details above are correct and I agree to be contacted about this test drive.
          </label>
          <p v-if="errors.consent" class="error-message">{{ errors.consent }}</p>
        </div>
      </div>

      <div class="button-row">
        <button class="primary-btn" type="submit">Submit Request</button>
        <button class="secondary-btn" type="button" @click="resetForm">Reset</button>
      </div>

      <p v-if="showSuccess" class="success-message" aria-live="polite">
        Request submitted successfully. The form will reset in 2 seconds.
      </p>
    </form>
  </section>
</template>

<script setup>
import { ref } from 'vue'

const props = defineProps({
  defaultName: {
    type: String,
    default: ''
  },
  formTitle: {
    type: String,
    default: 'Contact Us'
  }
})

const emit = defineEmits(['submit-form'])

const vehicleOptions = [
  'Toyota Camry Atara',
  'Mazda 3 Maxx',
  'Mitsubishi Lancer'
]

function initialForm() {
  return {
    name: props.defaultName,
    email: '',
    phone: '',
    budget: null,
    vehicle: '',
    preferredContact: '',
    date: '',
    time: '',
    message: '',
    consent: false
  }
}

const form = ref(initialForm())
const errors = ref({})
const showSuccess = ref(false)

function validateForm() {
  const nextErrors = {}

  if (!form.value.name) nextErrors.name = 'Please enter your full name.'
  if (!form.value.email || !/^\S+@\S+\.\S+$/.test(form.value.email)) {
    nextErrors.email = 'Please enter a valid email address.'
  }
  if (!form.value.phone) nextErrors.phone = 'Please enter your phone number.'
  if (!form.value.budget || form.value.budget < 1000) nextErrors.budget = 'Please enter a valid budget of at least $1,000.'
  if (!form.value.vehicle) nextErrors.vehicle = 'Please select a vehicle.'
  if (!form.value.preferredContact) nextErrors.preferredContact = 'Please choose a contact method.'
  if (!form.value.date) nextErrors.date = 'Please choose a preferred date.'
  if (!form.value.time) nextErrors.time = 'Please choose a preferred time.'
  if (!form.value.consent) nextErrors.consent = 'You must agree before submitting.'

  errors.value = nextErrors
  return Object.keys(nextErrors).length === 0
}

function submitForm() {
  showSuccess.value = false

  if (!validateForm()) return

  emit('submit-form', { ...form.value })
  showSuccess.value = true

  window.setTimeout(() => {
    resetForm()
  }, 2000)
}

function resetForm() {
  form.value = initialForm()
  errors.value = {}
  showSuccess.value = false
}
</script>
