<script setup>
const testimonials = [
  {
    text: 'IT FSD menjadi tempat saya untuk belajar, berkembang, dan berproses. Keep solid, keep growing! 🚀',
    name: 'Haikal Muhammad',
    role: 'Backend Developer (3 tahun)',
    initial: 'H',
    color: '#6366f1',
  },
  {
    text: 'Lingkungan paling suportif yang pernah aku temui. Dari junior sampai lead, semua mau berbagi. Benar-benar departemen terbaik perusahaan.',
    name: 'Lutfi Nofal',
    role: 'Frontend Developer (1 tahun)',
    initial: 'L',
    color: '#22d3ee',
  },
  {
    text: 'Aku masuk tanpa pengalaman produk besar, sekarang memegang sistem yang dipakai ribuan orang sehari-hari. Growth-nya gila cepat.',
    name: 'Andrianata P T',
    role: 'Mobile Developer (3 tahun)',
    initial: 'A',
    color: '#f59e0b',
  },
]
</script>

<template>
  <section id="testimoni">
    <div class="container">
      <div class="text-center">
        <span class="eyebrow">Testimoni</span>
        <h2 class="section-title">Kata Mereka yang Ada di Sini</h2>
        <p class="section-desc">
          Tidak usah percaya kami — dengar langsung dari anggota tim.
        </p>
      </div>

      <div class="testi-grid mt-12">
        <div v-for="t in testimonials" :key="t.name" class="card testi-card">
          <div class="quote-mark">“</div>
          <p class="quote">{{ t.text }}</p>
          <div class="author">
            <div class="avatar" :style="{ background: t.color }">{{ t.initial }}</div>
            <div>
              <div class="name">{{ t.name }}</div>
              <div class="role">{{ t.role }}</div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.testi-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 24px;
}

.testi-card {
  position: relative;
  padding-top: 40px;
}

.quote-mark {
  position: absolute;
  top: 18px;
  right: 24px;
  font-size: 3.4rem;
  font-weight: 900;
  color: var(--primary);
  opacity: 0.5;
  line-height: 1;
}

.quote {
  color: var(--text);
  font-size: 0.98rem;
  margin-bottom: 24px;
}

.author {
  display: flex;
  align-items: center;
  gap: 12px;
}

.avatar {
  width: 44px;
  height: 44px;
  border-radius: 50%;
  display: grid;
  place-items: center;
  color: #0b1020;
  font-weight: 800;
}

.name {
  font-weight: 700;
  font-size: 0.95rem;
}

.role {
  color: var(--muted);
  font-size: 0.82rem;
}

@media (max-width: 900px) {
  .testi-grid {
    grid-template-columns: 1fr;
  }
}
</style>