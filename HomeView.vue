<template>
  <div>
    <section class="hero">
      <div class="container hero-grid">
        <div>
          <p class="eyebrow">Melbourne used-car specialists</p>
          <h1>Find a car that fits your life and your budget.</h1>
          <p>
            Browse practical, reliable vehicles with clear pricing, mileage and key details.
            When you find the right one, book a test drive in minutes.
          </p>
          <div class="button-row">
            <button class="primary-btn" type="button" @click="$emit('change-view', 'cars')">Browse Cars</button>
            <button class="secondary-btn" type="button" @click="$emit('change-view', 'contact')">Book Test Drive</button>
          </div>
        </div>
        <div class="hero-visual" aria-label="Stylised car illustration">
          <div class="car-shape">AUTOHUB</div>
        </div>
      </div>
    </section>

    <section class="container section-block">
      <h2>Why choose Melbourne AutoHub?</h2>
      <div class="card-grid three-col">
        <article class="info-card">
          <h3>Clear vehicle details</h3>
          <p>Compare model, year, mileage, price and important specifications before you visit.</p>
        </article>
        <article class="info-card">
          <h3>Melbourne focused</h3>
          <p>Local dealership support with convenient enquiries and test-drive bookings.</p>
        </article>
        <article class="info-card">
          <h3>Simple buying journey</h3>
          <p>Browse, compare and contact the dealership without unnecessary steps.</p>
        </article>
      </div>
    </section>
  </div>
</template>

<script setup>
defineEmits(['change-view'])
</script>
