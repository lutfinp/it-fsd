<script setup>
const features = ['Source Code', 'DevOps 101', 'Design Excellence']
</script>

<template>
  <section id="beranda" class="hero">
    <div class="container hero-inner">
      <div class="hero-left">
        <span class="eyebrow">⭐ Best Department 2026</span>
        <h1>
          Department <span class="grad">IT FSD</span>
          <br />
          Tempat Kode Bertemu Karya Terbaik
        </h1>
        <p>
          Frontend Software Development — tim yang tidak hanya menulis kode, tetapi
          membangun pengalaman, budaya, dan masa depan digital. Karena kami percaya,
          <em>departemen terbaik dimulai dari orang-orang terbaik.</em>
        </p>

        <div class="hero-actions">
          <a href="#join" class="btn">Gabung Tim Kami</a>
          <a href="#tentang" class="btn-ghost">Kenali Kami ⇣</a>
        </div>

        <div class="hero-tags">
          <span v-for="f in features" :key="f" class="tag">✓ {{ f }}</span>
        </div>
      </div>

      <div class="hero-right">
        <div class="window">
          <div class="window-bar">
            <span class="dot red"></span>
            <span class="dot yellow"></span>
            <span class="dot green"></span>
            <code>it-fsd / best-department.spec.js</code>
          </div>
          <pre class="window-body"><code><span class="k">const</span> <span class="v">team</span> = {</code>
<code>  <span class="p">nama</span>: <span class="s">'IT FSD'</span>,</code>
<code>  <span class="p">produk</span>: <span class="s">'Best-in-class'</span>,</code>
<code>  <span class="p">budaya</span>: <span class="s">'Kolaboratif'</span>,</code>
<code>  <span class="p">growth</span>: <span class="s">'Tanpa Batas'</span>,</code>
<code>};</code>
<code>&nbsp;</code>
<code><span class="k">export</span> <span class="k">default</span> <span class="v">team</span><span class="p">;</span> <span class="c">// ✨ no bugs, just vibes</span></code></pre>
        </div>
        <div class="window-badge">Best dept? <b>Obv.</b> ✦</div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.hero {
  min-height: 100vh;
  display: flex;
  align-items: center;
  padding: 140px 0 80px;
  background:
    radial-gradient(700px 380px at 85% 10%, rgba(34, 211, 238, 0.14), transparent 60%),
    radial-gradient(700px 420px at 10% 90%, rgba(99, 102, 241, 0.16), transparent 60%);
}

.hero-inner {
  display: grid;
  grid-template-columns: 1.1fr 0.9fr;
  gap: 64px;
  align-items: center;
}

.hero h1 {
  font-size: clamp(2.2rem, 5vw, 3.6rem);
  font-weight: 900;
  line-height: 1.12;
  margin-bottom: 22px;
}

.grad {
  background: var(--gradient);
  -webkit-background-clip: text;
  background-clip: text;
  color: transparent;
}

.hero p {
  color: var(--muted);
  font-size: 1.1rem;
  max-width: 520px;
  margin-bottom: 34px;
}

.hero-actions {
  display: flex;
  gap: 16px;
  flex-wrap: wrap;
  margin-bottom: 30px;
}

.btn-ghost {
  display: inline-block;
  padding: 14px 28px;
  border-radius: 999px;
  border: 1px solid var(--border);
  color: var(--text);
  font-weight: 700;
  transition: border-color 0.2s, background 0.2s;
}

.btn-ghost:hover {
  border-color: var(--accent);
  background: rgba(34, 211, 238, 0.08);
}

.hero-tags {
  display: flex;
  gap: 12px;
  flex-wrap: wrap;
}

.tag {
  font-size: 0.85rem;
  color: var(--muted);
  border: 1px solid var(--border);
  padding: 6px 14px;
  border-radius: 999px;
}

.window {
  background: var(--dark-soft);
  border: 1px solid var(--border);
  border-radius: 16px;
  overflow: hidden;
  box-shadow: 0 30px 80px rgba(0, 0, 0, 0.5);
  animation: float 6s ease-in-out infinite;
}

.window-bar {
  display: flex;
  align-items: center;
  gap: 8px;
  padding: 14px 18px;
  background: rgba(255, 255, 255, 0.03);
  border-bottom: 1px solid var(--border);
}

.dot {
  width: 12px;
  height: 12px;
  border-radius: 50%;
}
.dot.red { background: #f87171; }
.dot.yellow { background: #fbbf24; }
.dot.green { background: #34d399; }

.window-bar code {
  margin-left: 10px;
  font-size: 0.8rem;
  color: var(--muted);
}

.window-body {
  padding: 22px;
  font-family: 'Courier New', monospace;
  font-size: 0.95rem;
  line-height: 1.7;
  overflow-x: auto;
}

.k { color: #c084fc; }
.v { color: #fbbf24; }
.p { color: #60a5fa; }
.s { color: #34d399; }
.c { color: #64748b; }

.window-badge {
  margin-top: 24px;
  width: fit-content;
  padding: 10px 18px;
  border-radius: 999px;
  background: rgba(52, 211, 153, 0.1);
  border: 1px solid rgba(52, 211, 153, 0.3);
  color: var(--text);
  font-size: 0.9rem;
  animation: float 6s ease-in-out infinite 1.5s;
}

@media (max-width: 900px) {
  .hero {
    padding-top: 120px;
    text-align: center;
  }
  .hero-inner {
    grid-template-columns: 1fr;
    gap: 48px;
  }
  .hero p {
    margin-inline: auto;
  }
  .hero-actions,
  .hero-tags {
    justify-content: center;
  }
  .window-badge {
    margin-inline: auto;
  }
}
</style>