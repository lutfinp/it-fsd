<script setup>
const perks = [
  {
    icon: '💜',
    title: 'Budaya Kolaboratif',
    desc: 'Code review yang membangun, knowledge sharing mingguan, dan tim yang selalu siap berdiri satu untuk lainnya.',
  },
  {
    icon: '☕',
    title: 'Lingkungan Santai',
    desc: 'Pekerjaan serius, suasana santai. Flexible hour, snack unlimited, dan teman diskusi istirahat yang seru.',
  },
  {
    icon: '🌱',
    title: 'Peluang Bertumbuh',
    desc: 'Mentoring, workshop internal, dan exposure ke stack terbaru — karirmu berkembang secepat tim ini.',
  },
  {
    icon: '🛠️',
    title: 'Teknologi Modern',
    desc: 'Vue 3, TypeScript, dan tooling terbaik. Kerja dengan stack yang kamu banggakan, bukan yang menua.',
  },
  {
    icon: '🚀',
    title: 'Dampak Nyata',
    desc: 'Karya kami dipakai ribuan pengguna setiap hari. Setiap baris kode memberi dampak yang terasa.',
  },
  {
    icon: '🏆',
    title: 'Pengakuan',
    desc: 'Departemen terbaik 2025 & 2026. Membuktikan bahwa kerja keras berbanding lurus dengan penghargaan.',
  },
]
</script>

<template>
  <section id="keunggulan">
    <div class="container">
      <div class="text-center">
        <span class="eyebrow">Keunggulan Kami</span>
        <h2 class="section-title">Bukan Sekadar Departemen, Ini Rumah</h2>
        <p class="section-desc">
          Enam alasan mengapa orang-orang bangga menjadi bagian dari IT FSD.
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