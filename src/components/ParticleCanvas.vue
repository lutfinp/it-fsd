<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const canvasRef = ref(null)
let animationId = null
let ctx = null
let particles = []
let mouse = { x: -9999, y: -9999 }

let isMobile = false
let autoMoveAngle = 0
const autoMoveSpeed = 0.005
let lastTouchTime = 0
let touchActive = false
let touchTarget = { x: -9999, y: -9999 }

const CONFIG = {
  countDesktop: 180,
  countMobile: 55,
  maxDistDesktop: 180,
  maxDistMobile: 110,
  mouseRadiusDesktop: 240,
  mouseRadiusMobile: 120,
  particleSpeed: 0.5,
  particleSize: 2.0,
  color: '52, 207, 235',    // --primary #34cfeb
  accentColor: '56, 189, 248',
}

class Particle {
  constructor(w, h) {
    this.reset(w, h)
  }

  reset(w, h) {
    this.x = Math.random() * w
    this.y = Math.random() * h
    this.vx = (Math.random() - 0.5) * CONFIG.particleSpeed
    this.vy = (Math.random() - 0.5) * CONFIG.particleSpeed
    this.radius = Math.random() * CONFIG.particleSize + 0.8
    this.alpha = Math.random() * 0.45 + 0.3
  }

  update(w, h) {
    const activeMouseRadius = isMobile ? CONFIG.mouseRadiusMobile : CONFIG.mouseRadiusDesktop
    const pushForceScale = isMobile ? 0.25 : 0.5

    // Mouse repulsion
    const dx = this.x - mouse.x
    const dy = this.y - mouse.y
    const dist = Math.sqrt(dx * dx + dy * dy)

    if (dist < activeMouseRadius && dist > 0) {
      const force = (activeMouseRadius - dist) / activeMouseRadius
      this.vx += (dx / dist) * force * pushForceScale
      this.vy += (dy / dist) * force * pushForceScale
    }

    // Gentle particle anti-clumping (prevents particles from bunching up)
    const minParticleGap = isMobile ? 45 : 35
    for (let i = 0; i < particles.length; i++) {
      const other = particles[i]
      if (other === this) continue
      const pdx = this.x - other.x
      const pdy = this.y - other.y
      const pdistSq = pdx * pdx + pdy * pdy
      if (pdistSq < minParticleGap * minParticleGap && pdistSq > 0) {
        const pdist = Math.sqrt(pdistSq)
        const pforce = (minParticleGap - pdist) / minParticleGap * 0.04
        this.vx += (pdx / pdist) * pforce
        this.vy += (pdy / pdist) * pforce
      }
    }

    // Dampen velocity smoothly
    this.vx *= 0.97
    this.vy *= 0.97

    // Clamp speed
    const maxSpeed = CONFIG.particleSpeed * (isMobile ? 2.0 : 2.5)
    const speed = Math.sqrt(this.vx * this.vx + this.vy * this.vy)
    if (speed > maxSpeed) {
      this.vx = (this.vx / speed) * maxSpeed
      this.vy = (this.vy / speed) * maxSpeed
    }

    this.x += this.vx
    this.y += this.vy

    // Bounce on edges with padding
    const padding = 10
    if (this.x < padding) { this.x = padding; this.vx *= -1 }
    if (this.x > w - padding) { this.x = w - padding; this.vx *= -1 }
    if (this.y < padding) { this.y = padding; this.vy *= -1 }
    if (this.y > h - padding) { this.y = h - padding; this.vy *= -1 }
  }

  draw(ctx) {
    ctx.beginPath()
    ctx.arc(this.x, this.y, this.radius, 0, Math.PI * 2)
    ctx.fillStyle = `rgba(${CONFIG.color}, ${this.alpha})`
    ctx.fill()
  }
}

function initParticles(w, h) {
  const count = isMobile ? CONFIG.countMobile : CONFIG.countDesktop
  particles = Array.from({ length: count }, () => new Particle(w, h))
}

function drawConnections() {
  const activeMaxDist = isMobile ? CONFIG.maxDistMobile : CONFIG.maxDistDesktop
  const activeMouseRadius = isMobile ? CONFIG.mouseRadiusMobile : CONFIG.mouseRadiusDesktop

  for (let i = 0; i < particles.length; i++) {
    for (let j = i + 1; j < particles.length; j++) {
      const dx = particles[i].x - particles[j].x
      const dy = particles[i].y - particles[j].y
      const dist = Math.sqrt(dx * dx + dy * dy)

      if (dist < activeMaxDist) {
        const alpha = (1 - dist / activeMaxDist) * (isMobile ? 0.25 : 0.35)
        ctx.beginPath()
        ctx.moveTo(particles[i].x, particles[i].y)
        ctx.lineTo(particles[j].x, particles[j].y)
        ctx.strokeStyle = `rgba(${CONFIG.color}, ${alpha})`
        ctx.lineWidth = isMobile ? 0.6 : 0.8
        ctx.stroke()
      }
    }

    // Connect particles to mouse
    const dx = particles[i].x - mouse.x
    const dy = particles[i].y - mouse.y
    const dist = Math.sqrt(dx * dx + dy * dy)

    if (dist < activeMouseRadius) {
      const alpha = (1 - dist / activeMouseRadius) * (isMobile ? 0.5 : 0.7)
      ctx.beginPath()
      ctx.moveTo(particles[i].x, particles[i].y)
      ctx.lineTo(mouse.x, mouse.y)
      ctx.strokeStyle = `rgba(${CONFIG.accentColor}, ${alpha})`
      ctx.lineWidth = isMobile ? 0.9 : 1.2
      ctx.stroke()
    }
  }
}

function drawMouseGlow() {
  if (mouse.x < -100 || mouse.x > 9000) return
  const glowRadius = isMobile ? 50 : 80
  const grad = ctx.createRadialGradient(mouse.x, mouse.y, 0, mouse.x, mouse.y, glowRadius)
  grad.addColorStop(0, `rgba(${CONFIG.color}, ${isMobile ? 0.16 : 0.12})`)
  grad.addColorStop(1, `rgba(${CONFIG.color}, 0)`)
  ctx.beginPath()
  ctx.arc(mouse.x, mouse.y, glowRadius, 0, Math.PI * 2)
  ctx.fillStyle = grad
  ctx.fill()

  // Cursor dot
  ctx.beginPath()
  ctx.arc(mouse.x, mouse.y, isMobile ? 2.5 : 3, 0, Math.PI * 2)
  ctx.fillStyle = `rgba(${CONFIG.color}, 0.9)`
  ctx.fill()
}

function updateMousePosition(w, h) {
  if (isMobile) {
    const now = Date.now()
    // If user touched recently (within 1.5s), lerp towards touch target
    if (touchActive || now - lastTouchTime < 1500) {
      if (touchTarget.x !== -9999) {
        mouse.x += (touchTarget.x - mouse.x) * 0.08
        mouse.y += (touchTarget.y - mouse.y) * 0.08
      }
    } else {
      // Smooth autonomous roaming around full mobile canvas
      autoMoveAngle += autoMoveSpeed
      const cx = w * 0.5
      const cy = h * 0.45
      const rx = w * 0.38
      const ry = h * 0.32

      const targetX = cx + Math.sin(autoMoveAngle * 0.7) * rx + Math.cos(autoMoveAngle * 1.3) * (rx * 0.25)
      const targetY = cy + Math.sin(autoMoveAngle * 1.1) * ry + Math.sin(autoMoveAngle * 0.5) * (ry * 0.3)

      if (mouse.x === -9999 || mouse.x < -100) {
        mouse.x = targetX
        mouse.y = targetY
      } else {
        mouse.x += (targetX - mouse.x) * 0.035
        mouse.y += (targetY - mouse.y) * 0.035
      }
    }
  }
}

function loop() {
  const canvas = canvasRef.value
  if (!canvas) return

  const w = canvas.width
  const h = canvas.height

  updateMousePosition(w, h)

  ctx.clearRect(0, 0, w, h)

  drawConnections()
  drawMouseGlow()

  particles.forEach(p => {
    p.update(w, h)
    p.draw(ctx)
  })

  animationId = requestAnimationFrame(loop)
}

function resize() {
  const canvas = canvasRef.value
  if (!canvas) return
  canvas.width = window.innerWidth
  canvas.height = window.innerHeight
  const wasMobile = isMobile
  isMobile = window.innerWidth <= 768
  if (wasMobile !== isMobile) {
    initParticles(canvas.width, canvas.height)
  }
}

function onMouseMove(e) {
  if (!isMobile) {
    mouse.x = e.clientX
    mouse.y = e.clientY
  }
}

function onMouseLeave() {
  if (!isMobile) {
    mouse.x = -9999
    mouse.y = -9999
  }
}

function onTouchStart(e) {
  if (isMobile && e.touches && e.touches.length > 0) {
    touchActive = true
    lastTouchTime = Date.now()
    touchTarget.x = e.touches[0].clientX
    touchTarget.y = e.touches[0].clientY
  }
}

function onTouchMove(e) {
  if (isMobile && e.touches && e.touches.length > 0) {
    touchActive = true
    lastTouchTime = Date.now()
    touchTarget.x = e.touches[0].clientX
    touchTarget.y = e.touches[0].clientY
  }
}

function onTouchEnd() {
  if (isMobile) {
    touchActive = false
    lastTouchTime = Date.now()
  }
}

onMounted(() => {
  const canvas = canvasRef.value
  ctx = canvas.getContext('2d')

  resize()
  initParticles(canvas.width, canvas.height)
  loop()

  window.addEventListener('resize', resize)
  window.addEventListener('mousemove', onMouseMove)
  window.addEventListener('mouseleave', onMouseLeave)
  window.addEventListener('touchstart', onTouchStart, { passive: true })
  window.addEventListener('touchmove', onTouchMove, { passive: true })
  window.addEventListener('touchend', onTouchEnd)
})

onUnmounted(() => {
  cancelAnimationFrame(animationId)
  window.removeEventListener('resize', resize)
  window.removeEventListener('mousemove', onMouseMove)
  window.removeEventListener('mouseleave', onMouseLeave)
  window.removeEventListener('touchstart', onTouchStart)
  window.removeEventListener('touchmove', onTouchMove)
  window.removeEventListener('touchend', onTouchEnd)
})
</script>

<template>
  <canvas ref="canvasRef" class="particle-canvas" />
</template>

<style scoped>
.particle-canvas {
  position: fixed;
  inset: 0;
  z-index: 0;
  pointer-events: none;
  width: 100vw;
  height: 100vh;
}
</style>
