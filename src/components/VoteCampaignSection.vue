<script setup>
import { ref, computed, onMounted, onUnmounted } from 'vue'

const target = new Date('2026-10-15T23:59:59')
const now = ref(Date.now())

const diff = computed(() => Math.max(0, target.getTime() - now.value))

const timeLeft = computed(() => {
  const d = Math.floor(diff.value / 86400000)
  const h = Math.floor((diff.value % 86400000) / 3600000)
  const m = Math.floor((diff.value % 3600000) / 60000)
  const s = Math.floor((diff.value % 60000) / 1000)
  return { d, h, m, s }
})

const pad = (n) => String(n).padStart(2, '0')

const votes = ref(41273)
const goal = 50000
const progress = computed(() => Math.min(100, Math.round((votes.value / goal) * 100)))

let timer
onMounted(() => {
  timer = setInterval(() => {
    now.value = Date.now()
  }, 1000)
})
onUnmounted(() => clearInterval(timer))

const steps = [
  { no: '1', title: 'Masuk / Daftar', desc: 'Gunakan akun karyawan untuk bergabung ke portal voting perusahaan.' },
  { no: '2', title: 'Pilih IT FSD', desc: 'Temukan kategori Best Proactive Department, lalu klik IT FSD.' },
  { no: '3', title: 'Kunci Voting-mu', desc: 'Konfirmasi pilihanmu. Satu suara dari kamu berarti segalanya.' },
]

const reasons = ['Kami selalu inisiatif duluan', 'Respon cepat di setiap sprint', 'Ide tanpa henti untuk produk']
</script>

<template>
  <section id="vote" class="vote">
    <div class="container">
      <div class="vote-box">
        <div class="text-center">
          <span class="eyebrow">🗳️ Campaign 2026</span>
          <h2 class="section-title">
            Vote <span class="grad">IT FSD</span> sebagai
            Best Proactive Department
          </h2>
          <p class="section-desc">
            Proaktif bukan sekadar kata bagi kami — itu budaya. Bantu wujudkan
            kemenangan yang sudah layak kami raih dengan satu suara darimu.
          </p>
        </div>

        <!-- Countdown -->
        <div class="countdown">
          <div class="countdown-box">
            <span class="cd-num">{{ pad(timeLeft.d) }}</span>
            <span class="cd-label">Hari</span>
          </div>
          <span class="cd-sep">:</span>
          <div class="countdown-box">
            <span class="cd-num">{{ pad(timeLeft.h) }}</span>
            <span class="cd-label">Jam</span>
          </div>
          <span class="cd-sep">:</span>
          <div class="countdown-box">
            <span class="cd-num">{{ pad(timeLeft.m) }}</span>
            <span class="cd-label">Menit</span>
          </div>
          <span class="cd-sep">:</span>
          <div class="countdown-box">
            <span class="cd-num">{{ pad(timeLeft.s) }}</span>
            <span class="cd-label">Detik</span>
          </div>
        </div>

        <!-- Progress voting -->
        <div class="progress-wrap">
          <div class="progress-head">
            <span>{{ votes.toLocaleString('id-ID') }} suara terkumpul</span>
            <span>Target {{ goal.toLocaleString('id-ID') }}</span>
          </div>
          <div class="progress-track">
            <div class="progress-fill" :style="{ width: progress + '%' }">
              <span class="progress-tip">{{ progress }}%</span>
            </div>
          </div>
        </div>

        <div class="vote-cta">
          <a href="#" class="btn btn-vote" @click.prevent="false">🗳️ Vote IT FSD Sekarang</a>
          <a href="#join" class="btn-ghost">Ajukan Pertanyaan</a>
        </div>

        <!-- Alasan -->
        <div class="reasons">
          <span v-for="r in reasons" :key="r" class="reason-chip">✦ {{ r }}</span>
        </div>

        <!-- Langkah -->
        <div class="steps">
          <div v-for="s in steps" :key="s.no" class="step card">
            <span class="step-no">{{ s.no }}</span>
            <h3>{{ s.title }}</h3>
            <p>{{ s.desc }}</p>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.vote {
  background:
    radial-gradient(700px 400px at 50% 0%, rgba(245, 158, 11, 0.1), transparent 60%),
    var(--dark);
}

.vote-box {
  padding: 72px 0 0;
}

.countdown {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 14px;
  margin-top: 36px;
}

.countdown-box {
  background: var(--dark-soft);
  border: 1px solid var(--border);
  border-radius: 14px;
  padding: 16px 22px;
  min-width: 84px;
  text-align: center;
}

.cd-num {
  display: block;
  font-size: 2.2rem;
  font-weight: 900;
  background: var(--gradient);
  -webkit-background-clip: text;
  background-clip: text;
  color: transparent;
  line-height: 1;
}

.cd-label {
  font-size: 0.72rem;
  color: var(--muted);
  text-transform: uppercase;
  letter-spacing: 1px;
  margin-top: 4px;
  display: block;
}

.cd-sep {
  font-size: 2rem;
  font-weight: 900;
  color: var(--muted);
  padding-bottom: 18px;
}

.progress-wrap {
  max-width: 560px;
  margin: 36px auto 0;
}

.progress-head {
  display: flex;
  justify-content: space-between;
  font-size: 0.85rem;
  color: var(--muted);
  margin-bottom: 10px;
}

.progress-track {
  height: 14px;
  border-radius: 999px;
  background: rgba(255, 255, 255, 0.06);
  border: 1px solid var(--border);
  overflow: visible;
  position: relative;
}

.progress-fill {
  height: 100%;
  border-radius: 999px;
  background: var(--gradient);
  position: relative;
  transition: width 1s ease;
}

.progress-tip {
  position: absolute;
  top: 50%;
  right: -10px;
  transform: translateY(-50%);
  background: var(--text);
  color: var(--dark);
  font-size: 0.72rem;
  font-weight: 800;
  padding: 3px 8px;
  border-radius: 999px;
}

.vote-cta {
  display: flex;
  gap: 16px;
  justify-content: center;
  flex-wrap: wrap;
  margin-top: 40px;
}

.btn-vote {
  background: linear-gradient(135deg, #f59e0b, #ef4444);
  box-shadow: 0 8px 24px rgba(245, 158, 11, 0.35);
  animation: pulse 2s infinite;
}

.btn-vote:hover {
  box-shadow: 0 12px 32px rgba(245, 158, 11, 0.5);
}

@keyframes pulse {
  0%, 100% { transform: scale(1); }
  50% { transform: scale(1.04); }
}

.reasons {
  display: flex;
  gap: 12px;
  justify-content: center;
  flex-wrap: wrap;
  margin-top: 28px;
}

.reason-chip {
  font-size: 0.85rem;
  color: var(--text);
  border: 1px solid rgba(245, 158, 11, 0.4);
  background: rgba(245, 158, 11, 0.08);
  padding: 8px 16px;
  border-radius: 999px;
}

.steps {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 20px;
  margin-top: 64px;
}

.step {
  position: relative;
  text-align: left;
  padding: 28px 22px 28px 64px;
}

.step-no {
  position: absolute;
  left: 18px;
  top: 26px;
  width: 34px;
  height: 34px;
  display: grid;
  place-items: center;
  border-radius: 50%;
  background: var(--gradient);
  color: #fff;
  font-weight: 800;
  font-size: 1rem;
}

.step h3 {
  font-size: 1.05rem;
  margin-bottom: 8px;
}

.step p {
  color: var(--muted);
  font-size: 0.9rem;
}

@media (max-width: 860px) {
  .steps {
    grid-template-columns: 1fr;
  }
}

@media (max-width: 560px) {
  .countdown {
    gap: 8px;
  }
  .countdown-box {
    min-width: 68px;
    padding: 12px 14px;
  }
  .cd-num {
    font-size: 1.7rem;
  }
}
</style>