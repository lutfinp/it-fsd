<script setup>
import { ref } from 'vue'
import danaQrImg from '../assets/dana-qr.jpg'

const danaUrl = 'https://link.dana.id/danakaget?c=sh72x4g7w&r=etXzLC&orderId=20260915101214397415010300166066897283067'
const copied = ref(false)

function copyLink() {
  navigator.clipboard.writeText(danaUrl)
  copied.value = true
  setTimeout(() => {
    copied.value = false
  }, 3000)
}
</script>

<template>
  <section id="danakaget" class="dana-section">
    <div class="container">
      <div class="dana-box">
        <div class="dana-glow"></div>
        
        <div class="dana-header">
          <span class="eyebrow-dana">🎁 Exclusive Bonus</span>
          <h2>
            Klaim Saldo <span class="grad-dana">DANA Kaget</span> IT FSD!
          </h2>
          <p>
            Scan QR Code di bawah menggunakan HP kamu atau klik tombol langsung untuk mengklaim kejutan saldo DANA Kaget eksklusif.
          </p>
        </div>

        <div class="dana-content">
          <!-- QR Card -->
          <div class="qr-card">
            <div class="qr-badge">
              <span class="dana-icon">💙</span>
              <span>DANA KAGET</span>
            </div>
            
            <div class="qr-image-wrap">
              <img :src="danaQrImg" alt="DANA Kaget QR Code" class="qr-img" />
            </div>

            <span class="scan-tip">📷 Arahkan Kamera / Scanner DANA Ke Sini</span>
          </div>

          <!-- Actions & Links -->
          <div class="dana-info">
            <div class="info-badge">
              <span class="pulsing-dot"></span>
              <span>DANA Kaget Active</span>
            </div>

            <h3>Klaim Cepat & Praktis</h3>
            <p class="info-text">
              DANA Kaget siap diklaim sekarang. Pastikan aplikasi DANA milikmu sudah ter-install di smartphone.
            </p>

            <div class="dana-actions">
              <a
                :href="danaUrl"
                target="_blank"
                rel="noopener noreferrer"
                class="btn btn-dana"
              >
                📱 Klaim via Aplikasi DANA 🚀
              </a>

              <button class="btn-copy" @click="copyLink">
                <span v-if="!copied">📋 Salin Link DANA Kaget</span>
                <span v-else>✅ Link Berhasil Disalin!</span>
              </button>
            </div>

            <div class="dana-notice">
              <span>⚡ Note: Kuota terbatas. Klaim sekarang sebelum kehabisan!</span>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.dana-section {
  padding: 80px 0 120px;
  background: var(--dark);
  position: relative;
  overflow: hidden;
}

.dana-box {
  position: relative;
  background: linear-gradient(145deg, rgba(17, 26, 53, 0.95), rgba(11, 16, 32, 0.98));
  border: 1px solid rgba(52, 207, 235, 0.3);
  border-radius: 28px;
  padding: 56px 40px;
  box-shadow: 0 30px 90px rgba(0, 0, 0, 0.7), 0 0 50px rgba(52, 207, 235, 0.15);
  overflow: hidden;
}

.dana-glow {
  position: absolute;
  top: -120px;
  right: -120px;
  width: 350px;
  height: 350px;
  background: radial-gradient(circle, rgba(52, 207, 235, 0.25) 0%, rgba(17, 142, 234, 0.15) 50%, transparent 70%);
  filter: blur(40px);
  pointer-events: none;
}

.dana-header {
  text-align: center;
  max-width: 680px;
  margin: 0 auto 48px;
}

.eyebrow-dana {
  display: inline-block;
  font-size: 0.82rem;
  font-weight: 800;
  letter-spacing: 2px;
  text-transform: uppercase;
  color: #34cfeb;
  background: rgba(52, 207, 235, 0.12);
  padding: 6px 16px;
  border-radius: 999px;
  border: 1px solid rgba(52, 207, 235, 0.3);
  margin-bottom: 16px;
}

.dana-header h2 {
  font-size: clamp(2rem, 4.5vw, 2.8rem);
  font-weight: 900;
  line-height: 1.15;
  margin-bottom: 14px;
}

.grad-dana {
  background: linear-gradient(135deg, #34cfeb, #118eea);
  -webkit-background-clip: text;
  background-clip: text;
  color: transparent;
}

.dana-header p {
  color: var(--muted);
  font-size: 1.05rem;
  line-height: 1.6;
}

.dana-content {
  display: grid;
  grid-template-columns: 320px 1fr;
  gap: 48px;
  align-items: center;
  max-width: 900px;
  margin: 0 auto;
}

/* QR Card */
.qr-card {
  background: #ffffff;
  border-radius: 20px;
  padding: 24px;
  text-align: center;
  box-shadow: 0 20px 50px rgba(0, 0, 0, 0.4), 0 0 30px rgba(52, 207, 235, 0.3);
  position: relative;
  transition: transform 0.3s ease;
}

.qr-card:hover {
  transform: translateY(-6px);
}

.qr-badge {
  display: inline-flex;
  align-items: center;
  gap: 6px;
  background: #118eea;
  color: #ffffff;
  font-weight: 800;
  font-size: 0.8rem;
  padding: 6px 14px;
  border-radius: 999px;
  margin-bottom: 16px;
  letter-spacing: 0.5px;
}

.qr-image-wrap {
  position: relative;
  width: 220px;
  height: 220px;
  margin: 0 auto 14px;
  border-radius: 12px;
  overflow: hidden;
  border: 2px solid #e2e8f0;
  background: #ffffff;
  display: flex;
  align-items: center;
  justify-content: center;
}

.qr-img {
  width: 100%;
  height: 100%;
  object-fit: contain;
  display: block;
}

.scan-line {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  height: 3px;
  background: linear-gradient(90deg, transparent, #34cfeb, #118eea, transparent);
  box-shadow: 0 0 12px #34cfeb;
  animation: scan 2.5s ease-in-out infinite;
}

@keyframes scan {
  0% { top: 0%; }
  50% { top: 96%; }
  100% { top: 0%; }
}

.scan-tip {
  display: block;
  font-size: 0.76rem;
  font-weight: 700;
  color: #64748b;
  margin-top: 4px;
}

/* Dana Info */
.dana-info {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
}

.info-badge {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  font-size: 0.82rem;
  font-weight: 700;
  color: #34d399;
  background: rgba(52, 211, 153, 0.1);
  border: 1px solid rgba(52, 211, 153, 0.3);
  padding: 5px 14px;
  border-radius: 999px;
  margin-bottom: 16px;
}

.pulsing-dot {
  width: 8px;
  height: 8px;
  border-radius: 50%;
  background: #34d399;
  box-shadow: 0 0 10px #34d399;
  animation: pulseDot 1.5s infinite;
}

@keyframes pulseDot {
  0%, 100% { transform: scale(1); opacity: 1; }
  50% { transform: scale(1.4); opacity: 0.6; }
}

.dana-info h3 {
  font-size: 1.6rem;
  font-weight: 800;
  color: var(--text);
  margin-bottom: 10px;
}

.info-text {
  color: var(--muted);
  font-size: 1rem;
  line-height: 1.6;
  margin-bottom: 28px;
}

.dana-actions {
  display: flex;
  flex-direction: column;
  gap: 12px;
  width: 100%;
  max-width: 360px;
  margin-bottom: 20px;
}

.btn-dana {
  background: linear-gradient(135deg, #34cfeb, #118eea);
  color: #ffffff !important;
  font-weight: 800;
  text-align: center;
  font-size: 1rem;
  padding: 16px 28px;
  border-radius: 999px;
  box-shadow: 0 10px 30px rgba(17, 142, 234, 0.4);
  transition: transform 0.2s ease, box-shadow 0.2s ease;
}

.btn-dana:hover {
  transform: translateY(-2px);
  box-shadow: 0 14px 36px rgba(17, 142, 234, 0.6);
}

.btn-copy {
  background: rgba(255, 255, 255, 0.06);
  border: 1px solid var(--border);
  color: var(--text);
  font-weight: 700;
  font-size: 0.9rem;
  padding: 12px 24px;
  border-radius: 999px;
  cursor: pointer;
  transition: background 0.2s, border-color 0.2s;
}

.btn-copy:hover {
  background: rgba(52, 207, 235, 0.12);
  border-color: #34cfeb;
  color: #34cfeb;
}

.dana-notice {
  font-size: 0.82rem;
  color: #fbbf24;
  font-weight: 600;
}

@media (max-width: 860px) {
  .dana-box {
    padding: 40px 24px;
  }

  .dana-content {
    grid-template-columns: 1fr;
    gap: 36px;
    text-align: center;
  }

  .dana-info {
    align-items: center;
  }

  .dana-actions {
    max-width: 100%;
  }

  .qr-card {
    margin: 0 auto;
  }
}
</style>
