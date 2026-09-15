<script setup>
const year = new Date().getFullYear()

const columns = [
  {
    title: 'Departemen',
    links: ['Beranda', 'Tentang', 'Keunggulan', 'Tim', 'Testimoni'],
  },
  {
    title: 'Konten',
    links: ['Blog', 'Wiki Internal', 'Code Library', 'Roadmap'],
  },
  {
    title: 'Ikuti Kami',
    links: ['GitHub', 'Figma Community', 'Slack', 'LinkedIn'],
  },
]
</script>

<template>
  <footer class="footer">
    <!-- <div class="container footer-inner">
      <div class="footer-brand">
        <a href="#beranda" class="brand">
          <span class="brand-mark">&lt;/&gt;</span>
          <span>IT&nbsp;<strong>FSD</strong></span>
        </a>
        <!-- <p>
          Frontend Software Development — departemen terbaik. Karena kode kami
          berbicara, dan tim kami yang membuatnya hidup.
        </p> -->
      <!-- </div> -->

      <!-- <div v-for="col in columns" :key="col.title" class="footer-col">
        <h4>{{ col.title }}</h4>
        <a v-for="l in col.links" :key="l" :href="'#' + col.title.toLowerCase()"> {{ l }}</a>
      </div> -->
    <!-- </div> -->

    <div class="footer-bottom">
      <div class="container">
        <p>© {{ year }} IT FSD · Best Department. Dibuat dengan 💜.</p>
      </div>
    </div>
  </footer>
</template>

<style scoped>
.footer {
  background: var(--dark-soft);
  border-top: 1px solid var(--border);
  padding-top: 64px;
}

.footer-inner {
  display: grid;
  grid-template-columns: 1.6fr repeat(3, 1fr);
  gap: 40px;
  padding-bottom: 48px;
}

.brand {
  display: inline-flex;
  align-items: center;
  gap: 10px;
  font-weight: 600;
  font-size: 1.15rem;
  margin-bottom: 16px;
}

.brand-mark {
  display: grid;
  place-items: center;
  width: 36px;
  height: 36px;
  border-radius: 10px;
  background: var(--gradient);
  color: #fff;
  font-weight: 800;
  font-family: 'Courier New', monospace;
}

.footer-brand p {
  color: var(--muted);
  font-size: 0.92rem;
  max-width: 300px;
}

.footer-col h4 {
  margin-bottom: 14px;
  font-size: 0.95rem;
}

.footer-col a {
  display: block;
  color: var(--muted);
  font-size: 0.9rem;
  margin-bottom: 10px;
  transition: color 0.2s;
}

.footer-col a:hover {
  color: var(--accent);
}

.footer-bottom {
  border-top: 1px solid var(--border);
  padding: 22px 0;
}

.footer-bottom p {
  text-align: center;
  color: var(--muted);
  font-size: 0.85rem;
}

@media (max-width: 860px) {
  .footer-inner {
    grid-template-columns: 1fr 1fr;
  }
}

@media (max-width: 560px) {
  .footer-inner {
    grid-template-columns: 1fr;
  }
}
</style>