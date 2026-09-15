<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const scrolled = ref(false)
const menuOpen = ref(false)

const links = [
  { label: 'Beranda', href: '#beranda' },
  { label: 'Tentang', href: '#tentang' },
  { label: 'Keunggulan', href: '#keunggulan' },
  { label: 'Tim', href: '#tim' },
  { label: 'Vote', href: '#vote' },
  { label: 'Testimoni', href: '#testimoni' },
]

const onScroll = () => {
  scrolled.value = window.scrollY > 30
}

onMounted(() => {
  window.addEventListener('scroll', onScroll)
})
onUnmounted(() => {
  window.removeEventListener('scroll', onScroll)
})
</script>

<template>
  <header class="nav" :class="{ scrolled }">
    <div class="container nav-inner">
      <a href="#beranda" class="brand">
        <span class="brand-mark">&lt;/&gt;</span>
        <span>IT&nbsp;<strong>FSD</strong></span>
      </a>

      <nav class="nav-links" :class="{ open: menuOpen }">
        <a v-for="l in links" :key="l.href" :href="l.href" @click="menuOpen = false">
          {{ l.label }}
        </a>
        <a href="#join" class="btn btn-small" @click="menuOpen = false">Gabung Sekarang</a>
      </nav>

      <button class="hamburger" @click="menuOpen = !menuOpen" aria-label="Menu">
        <span :class="{ open: menuOpen }"></span>
        <span :class="{ open: menuOpen }"></span>
        <span :class="{ open: menuOpen }"></span>
      </button>
    </div>
  </header>
</template>

<style scoped>
.nav {
  position: fixed;
  inset: 0 0 auto 0;
  z-index: 50;
  padding: 18px 0;
  transition: background 0.3s ease, padding 0.3s ease, border-color 0.3s ease;
  border-bottom: 1px solid transparent;
}

.nav.scrolled {
  background: rgba(11, 16, 32, 0.85);
  backdrop-filter: blur(12px);
  padding: 12px 0;
  border-color: var(--border);
}

.nav-inner {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.brand {
  display: flex;
  align-items: center;
  gap: 10px;
  font-size: 1.15rem;
  font-weight: 600;
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
  font-size: 0.85rem;
}

.nav-links {
  display: flex;
  align-items: center;
  gap: 28px;
}

.nav-links a {
  color: var(--text);
  font-size: 0.95rem;
  font-weight: 500;
  opacity: 0.85;
  transition: opacity 0.2s;
}

.nav-links a:hover {
  opacity: 1;
}

.btn {
  display: inline-block;
  padding: 14px 28px;
  border-radius: 999px;
  font-weight: 700;
  background: var(--gradient);
  color: #fff !important;
  box-shadow: 0 8px 24px rgba(99, 102, 241, 0.35);
  transition: transform 0.2s ease, box-shadow 0.2s ease;
}

.btn:hover {
  transform: translateY(-2px);
  box-shadow: 0 12px 28px rgba(99, 102, 241, 0.5);
}

.btn-small {
  padding: 10px 22px;
  font-size: 0.9rem;
  opacity: 1 !important;
}

.hamburger {
  display: none;
  flex-direction: column;
  gap: 5px;
  background: transparent;
  border: 0;
  cursor: pointer;
  padding: 6px;
}

.hamburger span {
  width: 24px;
  height: 2px;
  background: var(--text);
  border-radius: 2px;
  transition: transform 0.3s ease, opacity 0.3s ease;
}

.hamburger span.open:nth-child(1) {
  transform: translateY(7px) rotate(45deg);
}
.hamburger span.open:nth-child(2) {
  opacity: 0;
}
.hamburger span.open:nth-child(3) {
  transform: translateY(-7px) rotate(-45deg);
}

@media (max-width: 860px) {
  .hamburger {
    display: flex;
  }

  .nav-links {
    position: absolute;
    top: 100%;
    left: 0;
    right: 0;
    flex-direction: column;
    gap: 20px;
    padding: 28px 6%;
    background: rgba(11, 16, 32, 0.97);
    border-bottom: 1px solid var(--border);
    transform: translateY(-12px);
    opacity: 0;
    pointer-events: none;
    transition: opacity 0.3s ease, transform 0.3s ease;
  }

  .nav-links.open {
    opacity: 1;
    pointer-events: auto;
    transform: translateY(0);
  }
}
</style>