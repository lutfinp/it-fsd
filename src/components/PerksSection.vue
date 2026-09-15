<script setup>
const perks = [
  {
    icon: '🎯',
    title: 'End-to-End Solution',
    desc: 'Memahami kebutuhan dari awal hingga implementasi, mulai dari requirement, development, testing, troubleshooting, sampai sistem dapat digunakan oleh user.',
  },
  {
    icon: '🔄',
    title: 'Continuous Improvement',
    desc: 'Terus mengevaluasi sistem dan proses yang berjalan untuk menemukan peluang automasi, integrasi, dan pengembangan yang lebih efektif.',
  },
  {
    icon: '💡',
    title: 'Solusi Proaktif',
    desc: 'Tidak hanya menjalankan requirement, tetapi memberikan alternatif dan masukan teknis ketika terdapat proses yang masih dapat dibuat lebih sederhana dan efektif.',
  },
  {
    icon: '🤝',
    title: 'Kolaborasi',
    desc: 'Bekerja bersama IT PM, user, dan Department terkait melalui diskusi, testing, evaluasi, serta tindak lanjut sampai solusi berjalan sesuai kebutuhan.',
  },
  {
    icon: '🚀',
    title: 'Dampak Nyata',
    desc: 'Improvement membantu mengurangi pekerjaan manual, meningkatkan konsistensi data, dan membuat proses operasional lebih terstruktur.',
  },
  {
    icon: '♾️',
    title: 'Berkelanjutan',
    desc: 'Sistem tidak berhenti setelah implementasi, tetapi terus dipelihara dan dikembangkan mengikuti perubahan kebutuhan perusahaan.',
  },
]
</script>

<template>
  <section id="keunggulan">
    <div class="container">
      <div class="text-center">
        <span class="eyebrow">Keunggulan Kami</span>
        <h2 class="section-title">Bukan Sekadar Development, Kami Memberikan Dampak</h2>
        <p class="section-desc">
          Setiap improvement dimulai dari kebutuhan dan berakhir pada solusi
          yang memberikan manfaat nyata.
        </p>
      </div>

      <div class="perks-grid mt-12">
        <div v-for="p in perks" :key="p.title" class="card perk-card">
          <div class="icon">{{ p.icon }}</div>
          <h3>{{ p.title }}</h3>
          <p>{{ p.desc }}</p>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.perks-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 24px;
}

.icon {
  font-size: 2rem;
  margin-bottom: 14px;
}

.perk-card h3 {
  margin-bottom: 10px;
  font-size: 1.15rem;
}

.perk-card p {
  color: var(--muted);
  font-size: 0.95rem;
}

@media (max-width: 900px) {
  .perks-grid {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (max-width: 600px) {
  .perks-grid {
    grid-template-columns: 1fr;
  }
}
</style>