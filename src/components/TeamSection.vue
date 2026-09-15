<script setup>
const manager = {
  name: 'Efendi',
  role: 'Manager IT FSD',
  stack: ['Vue 3', 'Frappe', 'Architecture', 'Mentoring'],
  grad: 'linear-gradient(135deg,#6366f1,#22d3ee)',
}

const supervisors = [
  { name: 'Erland', role: 'Supervisor', grad: 'linear-gradient(135deg,#6366f1,#8b5cf6)' },
]

const staff = [
  { name: 'Lutfi Nofal', role: 'Frontend Developer', grad: 'linear-gradient(135deg,#6366f1,#22d3ee)' },
  { name: 'Andrianata', role: 'Frontend Developer', grad: 'linear-gradient(135deg,#ec4899,#8b5cf6)' },
  { name: 'Rofi', role: 'Backend Developer', grad: 'linear-gradient(135deg,#10b981,#f59e0b)' },
  { name: 'Atha Fajar', role: 'Backend Developer', grad: 'linear-gradient(135deg,#f59e0b,#22d3ee)' },
  { name: 'Haikal', role: 'Backend Developer', grad: 'linear-gradient(135deg,#8b5cf6,#ec4899)' },
  { name: 'Ian Hermawan', role: 'Backend Developer', grad: 'linear-gradient(135deg,#22d3ee,#ec4899)' },
]

const initials = (name) =>
  name
    .split(' ')
    .map((n) => n[0])
    .join('')
</script>

<template>
  <section id="tim" class="team">
    <div class="container">
      <div class="text-center">
        <span class="eyebrow">Struktur Tim</span>
        <h2 class="section-title">Hierarki Departemen IT FSD</h2>
        <p class="section-desc">
          Satu arah, satu visi. Dari manager hingga staff, setiap level punya peran
          penting untuk menjaga IT FSD tetap menjadi yang terbaik.
        </p>
      </div>

      <div class="hierarchy mt-12">
        <!-- Level 1: Manager -->
        <span class="level-label">1 Manager</span>

        <div class="manager-node">
          <div class="manager-card card">
            <div class="avatar" :style="{ background: manager.grad }">{{ initials(manager.name) }}</div>
            <h3>{{ manager.name }}</h3>
            <p class="role">{{ manager.role }}</p>
            <div class="stack">
              <span v-for="s in manager.stack" :key="s">{{ s }}</span>
            </div>
          </div>
        </div>

        <!-- Connector -->
        <div class="connector">
          <span class="connector-pill">1 Supervisor</span>
        </div>

        <!-- Level 2: Supervisors -->
        <div class="level-scroll">
          <div class="level">
            <div v-for="s in supervisors" :key="s.name" class="node">
              <div class="node-card card">
                <div class="avatar sm" :style="{ background: s.grad }">{{ initials(s.name) }}</div>
                <h4>{{ s.name }}</h4>
                <p class="role">{{ s.role }}</p>
              </div>
            </div>
          </div>
        </div>

        <!-- Connector -->
        <div class="connector">
          <span class="connector-pill">7 Staff</span>
        </div>

        <!-- Level 3: Staff -->
        <div class="level-scroll">
          <div class="level">
            <div v-for="s in staff" :key="s.name" class="node">
              <div class="node-card card">
                <div class="avatar sm" :style="{ background: s.grad }">{{ initials(s.name) }}</div>
                <h4>{{ s.name }}</h4>
                <p class="role">{{ s.role }}</p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.team {
  background: var(--dark-soft);
  border-block: 1px solid var(--border);
}

.hierarchy {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.field-group {
  width: 100%;
}

/* ---- Level labels (Manager / Supervisor / Staff) ---- */
.level-label {
  font-size: 0.78rem;
  font-weight: 700;
  letter-spacing: 1.5px;
  text-transform: uppercase;
  color: var(--muted);
  border: 1px solid var(--border);
  background: rgba(99, 102, 241, 0.08);
  padding: 6px 16px;
  border-radius: 999px;
  margin-bottom: 24px;
}

/* ---- Manager card ---- */
.manager-node {
  width: 100%;
  margin-bottom: 0;
}

.manager-card {
  width: 260px;
  margin-inline: auto;
  text-align: center;
  padding: 32px 24px;
  border-color: rgba(99, 102, 241, 0.5);
  box-shadow: 0 20px 60px rgba(99, 102, 241, 0.25);
}

.avatar {
  width: 76px;
  height: 76px;
  margin: 0 auto 14px;
  border-radius: 50%;
  display: grid;
  place-items: center;
  font-size: 1.4rem;
  font-weight: 800;
  color: #fff;
  box-shadow: 0 8px 24px rgba(0, 0, 0, 0.3);
}

.avatar.sm {
  width: 52px;
  height: 52px;
  font-size: 1rem;
}

.manager-card h3 {
  font-size: 1.25rem;
  margin-bottom: 4px;
}

.role {
  color: var(--muted);
  font-size: 0.85rem;
  margin-bottom: 14px;
}

.stack {
  display: flex;
  gap: 6px;
  justify-content: center;
  flex-wrap: wrap;
}

.stack span {
  font-size: 0.72rem;
  padding: 4px 10px;
  border-radius: 999px;
  background: rgba(34, 211, 238, 0.12);
  color: var(--accent);
}

/* ---- Connector between levels ---- */
.connector {
  position: relative;
  width: 2px;
  height: 64px;
  background: linear-gradient(
    to bottom,
    rgba(99, 102, 241, 0.9),
    rgba(34, 211, 238, 0.9)
  );
}

.connector-pill {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  background: var(--dark);
  border: 1px solid var(--border);
  padding: 5px 16px;
  border-radius: 999px;
  font-size: 0.8rem;
  font-weight: 700;
  color: var(--text);
  white-space: nowrap;
  z-index: 1;
}

/* ---- Scrolling level row ---- */
.level-scroll {
  width: 100%;
  overflow-x: auto;
  scrollbar-width: none;
}

.level-scroll::-webkit-scrollbar {
  display: none;
}

.level {
  display: flex;
  justify-content: center;
  gap: 16px;
  width: max-content;
  min-width: 100%;
  position: relative;
  padding-top: 48px;
  padding-bottom: 6px;
}

/* horizontal backbone */
.level::before {
  content: '';
  position: absolute;
  top: 0;
  left: 1%;
  right: 1%;
  height: 2px;
  background: linear-gradient(90deg, rgba(99, 102, 241, 0.9), rgba(34, 211, 238, 0.9));
}

.node {
  position: relative;
  flex: 0 0 auto;
  width: 178px;
}

/* vertical stem from backbone to card */
.node::before {
  content: '';
  position: absolute;
  top: -48px;
  left: 50%;
  width: 2px;
  height: 48px;
  background: rgba(99, 102, 241, 0.8);
  transform: translateX(-50%);
}

.node-card {
  text-align: center;
  padding: 24px 16px;
}

.node-card h4 {
  font-size: 0.98rem;
  margin-bottom: 4px;
}

.node-card .role {
  font-size: 0.78rem;
  margin-bottom: 0;
  min-height: 2.4em;
}

@media (max-width: 600px) {
  .manager-card {
    width: 220px;
  }
}
</style>