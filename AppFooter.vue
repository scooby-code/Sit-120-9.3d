<template>
  <footer class="site-footer">
    <div class="container footer-grid">
      <div>
        <h3>Melbourne AutoHub</h3>
        <p>Helping Melbourne drivers find the right car with clear information and friendly service.</p>
      </div>

      <div>
        <h3>Contact</h3>
        <p>221 Burwood Highway, Burwood VIC 3125</p>
        <p>Phone: (03) 9000 1200</p>
        <p>Email: hello@melbourneautohub.example</p>
      </div>

      <div>
        <h3>Quick Links</h3>
        <button type="button" @click="$emit('change-view', 'home')">Home</button>
        <button type="button" @click="$emit('change-view', 'cars')">Cars</button>
        <button type="button" @click="$emit('change-view', 'contact')">Book a Test Drive</button>
      </div>
    </div>
    <p class="copyright">&copy; 2026 Melbourne AutoHub. All rights reserved.</p>
  </footer>
</template>

<script setup>
defineEmits(['change-view'])
</script>
