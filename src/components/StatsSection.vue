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

      <div class="about-cards">
        <div class="about-card">
          <div class="about-card-icon">⚙️</div>
          <div class="about-card-body">
            <h4>Optimasi Berkelanjutan</h4>
            <p>
              IT FSD melihat peluang nyata untuk meningkatkan proses melalui
              <span class="highlight">automasi</span>,
              <span class="highlight">integrasi</span>,
              pengembangan fitur, dan penyesuaian sistem agar semakin sesuai
              dengan kebutuhan operasional perusahaan.
            </p>
          </div>
        </div>

        <div class="about-card">
          <div class="about-card-icon">🏗️</div>
          <div class="about-card-body">
            <h4>Ekosistem Sistem Internal</h4>
            <p>
              Sistem seperti
              <span class="highlight">ELITE</span>,
              <span class="highlight">LMS</span>,
              <span class="highlight">HRMS</span>,
              <span class="highlight">HRIS</span>,
              dan berbagai aplikasi internal menjadi tulang punggung aktivitas perusahaan.
              IT FSD berkomitmen menjaga stabilitas, melakukan improvement, dan memastikan
              setiap sistem terus berkembang mengikuti kebutuhan bisnis.
            </p>
          </div>
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

  .about-cards {
    grid-template-columns: 1fr;
  }
}

@media (max-width: 480px) {
  .stats-grid {
    grid-template-columns: repeat(2, 1fr);
    gap: 12px;
  }
  .stat-value {
    font-size: 2rem;
  }
  .about-card {
    flex-direction: column;
    gap: 14px;
    padding: 20px;
  }
  .about-card-icon {
    width: 44px;
    height: 44px;
    font-size: 1.6rem;
  }
}

/* About Cards */
.about-cards {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 24px;
  margin-top: 48px;
}

.about-card {
  display: flex;
  gap: 20px;
  align-items: flex-start;
  background: rgba(255, 255, 255, 0.03);
  border: 1px solid var(--border);
  border-radius: 20px;
  padding: 28px 28px;
  position: relative;
  overflow: hidden;
  transition: border-color 0.3s ease, transform 0.3s ease, box-shadow 0.3s ease;
}

.about-card::before {
  content: '';
  position: absolute;
  inset: 0;
  background: linear-gradient(135deg, rgba(52, 207, 235, 0.06), transparent 60%);
  opacity: 0;
  transition: opacity 0.3s ease;
}

.about-card:hover {
  border-color: rgba(52, 207, 235, 0.4);
  transform: translateY(-4px);
  box-shadow: 0 16px 48px rgba(0, 0, 0, 0.3), 0 0 24px rgba(52, 207, 235, 0.08);
}

.about-card:hover::before {
  opacity: 1;
}

.about-card-icon {
  font-size: 2rem;
  line-height: 1;
  flex-shrink: 0;
  width: 52px;
  height: 52px;
  display: grid;
  place-items: center;
  background: rgba(52, 207, 235, 0.1);
  border: 1px solid rgba(52, 207, 235, 0.2);
  border-radius: 14px;
}

.about-card-body h4 {
  font-size: 1.05rem;
  font-weight: 700;
  color: var(--text);
  margin-bottom: 10px;
}

.about-card-body p {
  color: var(--muted);
  font-size: 0.95rem;
  line-height: 1.75;
}

.highlight {
  color: #34cfeb;
  font-weight: 600;
  background: rgba(52, 207, 235, 0.1);
  padding: 1px 6px;
  border-radius: 5px;
}

</style>