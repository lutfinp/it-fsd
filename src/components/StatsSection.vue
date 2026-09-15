<script setup>
const stats = [
  { value: '40+', label: 'Engineer & Designers' },
  { value: '50+', label: 'Produk & Fitur Dirilis' },
  { value: '98%', label: 'Kepuasan Anggota' },
  { value: '100%', label: 'Bersemangat Setiap Pagi' },
]
</script>

<template>
  <section id="tentang" class="stats">
    <div class="container">
      <div class="text-center">
        <span class="eyebrow">Kenapa IT FSD?</span>
        <h2 class="section-title">Angka yang Berbicara</h2>
        <p class="section-desc">
          Prestasi adalah bukti. Berikut capaian yang menjadikan IT FSD
          departemen terbaik di antara yang terbaik.
        </p>
      </div>

      <div class="stats-grid mt-12">
        <div v-for="s in stats" :key="s.label" class="stat-card card">
          <div class="stat-value grad">{{ s.value }}</div>
          <div class="stat-label">{{ s.label }}</div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.stats {
  background: var(--dark-soft);
  border-block: 1px solid var(--border);
}

.stats-grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 24px;
}

.stat-card {
  text-align: center;
  padding: 34px 20px;
}

.stat-value {
  font-size: 2.6rem;
  font-weight: 900;
  margin-bottom: 6px;
}

.stat-label {
  color: var(--muted);
  font-size: 0.92rem;
}

@media (max-width: 860px) {
  .stats-grid {
    grid-template-columns: repeat(2, 1fr);
  }
}
</style>