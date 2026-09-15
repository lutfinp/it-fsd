<script setup>
const stats = [
  {
    value: '01',
    label: 'Kebutuhan Bisnis',
  },
  {
    value: '02',
    label: 'Solusi Digital',
  },
  {
    value: '03',
    label: 'Improvement Berkelanjutan',
  },
  {
    value: '04',
    label: 'Dampak Nyata',
  },
]
</script>

<template>
  <section id="tentang" class="stats">
    <div class="container">
      <div class="text-center">
        <span class="eyebrow">Tentang IT FSD</span>
        <h2 class="section-title">Mengubah Kebutuhan Menjadi Solusi</h2>
        <p class="section-desc">
          Seiring berkembangnya kebutuhan bisnis, berbagai sistem yang digunakan
          oleh perusahaan perlu terus dikembangkan dan dioptimalkan.
        </p>
      </div>

      <div class="stats-grid mt-12">
        <div v-for="s in stats" :key="s.label" class="stat-card card">
          <div class="stat-value grad">{{ s.value }}</div>
          <div class="stat-label">{{ s.label }}</div>
        </div>
      </div>

      <div class="about-content">
        <p>
          IT FSD melihat adanya peluang untuk meningkatkan proses melalui
          automasi, integrasi, pengembangan fitur, dan penyesuaian sistem agar
          semakin sesuai dengan kebutuhan operasional.
        </p>

        <p>
          Sistem seperti ELITE, LMS, HRMS, HRIS, dan berbagai aplikasi internal
          memiliki peran penting dalam mendukung aktivitas perusahaan. Karena itu,
          IT FSD tidak hanya berfokus pada pengembangan fitur baru, tetapi juga
          menjaga stabilitas, melakukan improvement, dan memastikan sistem dapat
          terus berkembang mengikuti kebutuhan bisnis.
        </p>
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