<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const canvasRef = ref(null)
let animationId = null
let ctx = null
let particles = []
let mouse = { x: -9999, y: -9999 }

const CONFIG = {
  count: 180,
  maxDist: 180,
  mouseRadius: 260,
  particleSpeed: 0.6,
  particleSize: 2.2,
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
    this.alpha = Math.random() * 0.5 + 0.3
  }

  update(w, h) {
    // Mouse repulsion
    const dx = this.x - mouse.x
    const dy = this.y - mouse.y
    const dist = Math.sqrt(dx * dx + dy * dy)

    if (dist < CONFIG.mouseRadius) {
      const force = (CONFIG.mouseRadius - dist) / CONFIG.mouseRadius
      this.vx += (dx / dist) * force * 0.6
      this.vy += (dy / dist) * force * 0.6
    }

    // Dampen velocity
    this.vx *= 0.98
    this.vy *= 0.98

    // Clamp speed
    const speed = Math.sqrt(this.vx * this.vx + this.vy * this.vy)
    if (speed > CONFIG.particleSpeed * 3) {
      this.vx = (this.vx / speed) * CONFIG.particleSpeed * 3
      this.vy = (this.vy / speed) * CONFIG.particleSpeed * 3
    }

    this.x += this.vx
    this.y += this.vy

    // Bounce on edges
    if (this.x < 0 || this.x > w) this.vx *= -1
    if (this.y < 0 || this.y > h) this.vy *= -1
    this.x = Math.max(0, Math.min(w, this.x))
    this.y = Math.max(0, Math.min(h, this.y))
  }

  draw(ctx) {
    ctx.beginPath()
    ctx.arc(this.x, this.y, this.radius, 0, Math.PI * 2)
    ctx.fillStyle = `rgba(${CONFIG.color}, ${this.alpha})`
    ctx.fill()
  }
}

function initParticles(w, h) {
  particles = Array.from({ length: CONFIG.count }, () => new Particle(w, h))
}

function drawConnections() {
  for (let i = 0; i < particles.length; i++) {
    for (let j = i + 1; j < particles.length; j++) {
      const dx = particles[i].x - particles[j].x
      const dy = particles[i].y - particles[j].y
      const dist = Math.sqrt(dx * dx + dy * dy)

      if (dist < CONFIG.maxDist) {
        const alpha = (1 - dist / CONFIG.maxDist) * 0.35
        ctx.beginPath()
        ctx.moveTo(particles[i].x, particles[i].y)
        ctx.lineTo(particles[j].x, particles[j].y)
        ctx.strokeStyle = `rgba(${CONFIG.color}, ${alpha})`
        ctx.lineWidth = 0.8
        ctx.stroke()
      }
    }

    // Connect particles to mouse
    const dx = particles[i].x - mouse.x
    const dy = particles[i].y - mouse.y
    const dist = Math.sqrt(dx * dx + dy * dy)

    if (dist < CONFIG.mouseRadius) {
      const alpha = (1 - dist / CONFIG.mouseRadius) * 0.7
      ctx.beginPath()
      ctx.moveTo(particles[i].x, particles[i].y)
      ctx.lineTo(mouse.x, mouse.y)
      ctx.strokeStyle = `rgba(${CONFIG.accentColor}, ${alpha})`
      ctx.lineWidth = 1.2
      ctx.stroke()
    }
  }
}

function drawMouseGlow() {
  if (mouse.x < 0 || mouse.x > 9000) return
  const grad = ctx.createRadialGradient(mouse.x, mouse.y, 0, mouse.x, mouse.y, 80)
  grad.addColorStop(0, `rgba(${CONFIG.color}, 0.12)`)
  grad.addColorStop(1, `rgba(${CONFIG.color}, 0)`)
  ctx.beginPath()
  ctx.arc(mouse.x, mouse.y, 80, 0, Math.PI * 2)
  ctx.fillStyle = grad
  ctx.fill()

  // Cursor dot
  ctx.beginPath()
  ctx.arc(mouse.x, mouse.y, 3, 0, Math.PI * 2)
  ctx.fillStyle = `rgba(${CONFIG.color}, 0.9)`
  ctx.fill()
}

function loop() {
  const canvas = canvasRef.value
  if (!canvas) return

  const w = canvas.width
  const h = canvas.height

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
}

function onMouseMove(e) {
  mouse.x = e.clientX
  mouse.y = e.clientY
}

function onMouseLeave() {
  mouse.x = -9999
  mouse.y = -9999
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
})

onUnmounted(() => {
  cancelAnimationFrame(animationId)
  window.removeEventListener('resize', resize)
  window.removeEventListener('mousemove', onMouseMove)
  window.removeEventListener('mouseleave', onMouseLeave)
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
