<template>
  <section class="container section-block">
    <p class="eyebrow">Available vehicles</p>
    <h1>Browse Cars</h1>
    <p>Explore a selection of vehicles suited to different needs and budgets.</p>

    <div class="card-grid car-grid">
      <article v-for="car in cars" :key="car.name" class="car-card">
        <div class="car-image" :aria-label="`${car.name} illustration`">{{ car.short }}</div>
        <div class="car-card-body">
          <h2>{{ car.name }}</h2>
          <p class="price">${{ car.price.toLocaleString() }}</p>
          <ul>
            <li>{{ car.year }}</li>
            <li>{{ car.mileage.toLocaleString() }} km</li>
            <li>{{ car.transmission }}</li>
          </ul>
          <button class="primary-btn" type="button" @click="$emit('change-view', 'contact')">Book Test Drive</button>
        </div>
      </article>
    </div>
  </section>
</template>

<script setup>
defineEmits(['change-view'])

const cars = [
  { name: 'Toyota Camry Atara', short: 'CAMRY', price: 15990, year: 2015, mileage: 148000, transmission: 'Automatic' },
  { name: 'Mazda 3 Maxx', short: 'MAZDA 3', price: 13990, year: 2016, mileage: 132000, transmission: 'Automatic' },
  { name: 'Mitsubishi Lancer', short: 'LANCER', price: 11990, year: 2014, mileage: 156000, transmission: 'Automatic' }
]
</script>
